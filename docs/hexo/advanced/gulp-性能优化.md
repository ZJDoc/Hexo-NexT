
# [gulp]性能优化

使用[gulp](https://gulpjs.com/)以及插件来压缩`html/css/js/image`等静态资源，加快博客访问速度

`gulp`在版本`4.0.0`前后针对`JS`语法处理有区别，当前使用最新版本`4.0.2`

## 安装

```
$ npm install gulp -g
$ npm install --save gulp gulp-cli gulp-htmlclean gulp-htmlmin gulp-minify-css gulp-clean-css gulp-uglify gulp-imagemin
# 解决GulpUglifyError: unable to minify JavaScript
$ npm install babel-core@6.26.3 --save
$ npm install gulp-babel@7.0.1 --save
$ npm install babel-preset-es2015@6.24.1 --save
# gulp-babel 取消严格模式方法("use strict")
$ npm install babel-plugin-transform-remove-strict-mode --save
```

* `gulp-htmlclean`：清理`html`
* `gulp-htmlmin`：压缩`html`
* `gulp-minify-css`：压缩`css`
* `gulp-clean-css`：清理`css`
* `gulp-uglify`：混淆`js`
* `gulp-imagemin`：压缩图片

当前版本

```
$ gulp -v
CLI version: 2.3.0
Local version: 4.0.2
```

## 配置

编辑`gulpfile.js`文件，放置于`~/`

```
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');
var babel = require('gulp-babel');

// 压缩css文件
gulp.task('minify-css', function (done) {
    return gulp.src('./public/**/*.css')
        .pipe(minifycss())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩html文件
gulp.task('minify-html', function (done) {
    return gulp.src('./public/**/*.html')
        .pipe(htmlclean())
        .pipe(htmlmin({
            removeComments: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
        }))
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩js文件
gulp.task('minify-js', function (done) {
    return gulp.src(['./public/**/*.js', '!./public/**/*.min.js'])
        .pipe(babel({
            //将ES6代码转译为可执行的JS代码
            presets: ['es2015'] // es5检查机制
        }))
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩 public/images 目录内图片(Version<3)
// gulp.task('minify-images', function () {
//     gulp.src('./public/images/**/*.*')
//         .pipe(imagemin({
//             optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
//             progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
//             interlaced: false, //类型：Boolean 默认：false 隔行扫描gif进行渲染
//             multipass: false, //类型：Boolean 默认：false 多次优化svg直到完全优化
//         }))
//         .pipe(gulp.dest('./public/images'));
// });

// 压缩 public/images 目录内图片(Version>3)
gulp.task('minify-images', function (done) {
    gulp.src('./public/images/**/*.*')
        .pipe(imagemin([
            imagemin.gifsicle({interlaced: true}),
            // imagemin.jpegtran({progressive: true}),
            imagemin.mozjpeg({progressive: true}),
            imagemin.optipng({optimizationLevel: 5}),
            imagemin.svgo({
                plugins: [
                    {removeViewBox: true},
                    {cleanupIDs: false}
                ]
            })
        ]))
        .pipe(gulp.dest('./public/images'));
    done();
});

//4.0以前的写法 
//gulp.task('default', [
//  'minify-html', 'minify-css', 'minify-js', 'minify-images'
//]);
//4.0以后的写法
// 执行 gulp 命令时执行的任务
gulp.task('default', gulp.series(gulp.parallel('minify-html', 'minify-css', 'minify-js', 'minify-images')), function () {
    console.log("----------gulp Finished----------");
    // Do something after a, b, and c are finished.
});
```

新建`.babelrc`文件：

```
{
    'presets': ['es2015'],
    "plugins": ["transform-remove-strict-mode"]
}
```

## 执行

在运行完`hexo generate`后就可以执行`gulp`

```
$ hexo generate && gulp
INFO  Validating config
INFO  Start processing
INFO  Files loaded in 89 ms
INFO  0 files generated in 44 ms
[20:51:18] Using gulpfile ~/blogs/gulpfile.js
[20:51:18] Starting 'default'...
[20:51:18] Starting 'minify-html'...
[20:51:18] Starting 'minify-css'...
[20:51:18] Starting 'minify-js'...
[20:51:18] Starting 'minify-images'...
[20:51:18] Finished 'minify-images' after 122 ms
[20:51:19] gulp-imagemin: Minified 1 image (saved 57.9 kB - 63.1%)
[20:51:19] Finished 'minify-js' after 564 ms
[20:51:19] Finished 'minify-css' after 572 ms
[20:51:19] Finished 'minify-html' after 624 ms
[20:51:19] Finished 'default' after 625 ms
```

再执行`hexo server`即可

## `font-awesome`加载失败

`gulp`压缩完成后，如果图标显示出错，说明`font-awesome`加载失败。参考[小图标不显示 [check hexo-filter-optimize, and CDN configs maybe]](https://github.com/theme-next/hexo-filter-optimize/issues/10)和[ 添加插件后fontawesome图标失效 #8 ](https://github.com/theme-next/hexo-filter-optimize/issues/8)

有两种解决方案（*我使用第二种*）：

1. 取消`css`压缩

2. 使用`cdn`

修改主题`_config.yml`，添加

```
fontawesome: https://cdn.bootcss.com/font-awesome/4.6.2/css/font-awesome.min.css
```

## imagemin.jpegtran error

错误信息如下：

```
[20:16:58] TypeError: imagemin.jpegtran is not a function
    at /home/zj/blogs/gulpfile.js:60:22
    at minify-images (/home/zj/blogs/node_modules/_undertaker@1.3.0@undertaker/lib/set-task.js:13:15)
    at bound (domain.js:413:15)
    at runBound (domain.js:424:12)
    at asyncRunner (/home/zj/blogs/node_modules/_async-done@1.3.2@async-done/index.js:55:18)
    at processTicksAndRejections (internal/process/task_queues.js:75:11)
[20:16:58] 'default' errored after 30 ms
```

参考[TypeError: imagemin.jpegtran is not a function](https://blog.csdn.net/qq_33521184/article/details/106130601)，解决：

```
    // imagemin.jpegtran({progressive: true}),
    imagemin.mozjpeg({progressive: true}),
```

## 相关阅读

* [使用gulp插件加速hexo博客](https://blog.csdn.net/jinggege0818/article/details/82461795)

* [Hexo博客使用gulp压缩静态资源](https://segmentfault.com/a/1190000019842178)