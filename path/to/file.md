<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Task_runner</title>
<link rel="stylesheet" href="https://stackedit.io/res-min/themes/base.css" />
<style type="text/css">
.body{font-family:'Malgun Gothic', '맑은 고딕', sans-serif}
.container{max-width:45em}
li{margin-top:6px}
li:first-child{margin-top:0}
/* Print, PDF전환 전용 */
.pagebreak{page-break-after: always}
.pagefront{display:none;position:relative;height:249mm;margin:0;padding:0;}
.pagefront:before{display:table;content:'';}
.pagetitle{padding-top:2em;font-size:3em;}
.pagedesc{margin-top:3em;font-size:1.3em;color:#333;}
.pageauthor{margin-top:6em;color:#777}
.pageauthor span{display:block;}
.pageauthor .author{position:relative;padding-top:6px;color:#333}
.pageauthor .author:after{position:absolute;left:0;top:0;width:30px;height:4px;background-color:#ef2323;content:''}
.pageauthor .date{margin-top:4px;}
.pagefront .mark{position:absolute;left:0;bottom:0;width:100%;border-top:1px solid #777;text-align:right;letter-spacing:7px;color:#333;}
@media print {
  .pagefront{display:block;}
}
</style>
<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
</head>
<body><div class="container"><h2 id="프론트엔드-빌드-자동화-task-runner">프론트엔드 빌드 자동화 - task runner</h2>

<p><img src="http://postfiles16.naver.net/MjAxNjEyMDdfMTcw/MDAxNDgxMTAwMTI5MDUw.51_bUQsb1pc_Tg2d-4sHeqhgdX34uiTPLOWJ3MyR_Ocg.LKsWIc2NsJTwIokNZO7EBbIlXvffz4J4DEAFWhb8TWYg.PNG.yoplle/%EC%A0%9C%EB%AA%A9-%EC%97%86%EC%9D%8C-2.png?type=w2" alt="enter image description here" title=""></p>



<h3 id="modern-front-end-development-technology-stack">Modern front-end development technology stack</h3>

<blockquote>
  <ul>
  <li>Editors / IDE : Sublime Text, WebStorm, Atom, Vim, Brackets..</li>
  <li>Version control systems : Git, SVN, Mercurial..</li>
  <li>Package managers : npm, Bower..</li>
  <li>Linters : JSLint, JSHint, CSSLint..</li>
  <li>CSS preprocessors : SASS/SCSS, LESS, stylus..</li>
  <li>JavaScript preprocessors(transpilers) : CoffeeScript, TypeScript, Babel..</li>
  <li>Minificators : YUI Compressor, UglifyJS..</li>
  <li>task runners : Grunt, Gulp, Broccoli..</li>
  <li>CSS frameworks : Bootstrap, Semantic UI..</li>
  <li>JavaScript libraries : jQuery, Underscore, D3..</li>
  <li>JavaScript frameworks : Angular, React, Ember, Backbone, Knockout..</li>
  <li>Scaffolding : Yeoman..</li>
  <li>Web aplication platform : Firebase..</li>
  </ul>
</blockquote>

<hr>



<h3 id="task-runner">task runner</h3>

<blockquote>
  <p><strong>모던 웹을 작성한다고 할 때 어떤 일들이 필요한가:</strong></p>
  
  <ul>
  <li>LESS 또는 SASS 파일을 CSS로 컴파일하기</li>
  <li>CoffeeScript 또는 TypeScript를 자바스크립트 파일로 컴파일 하기</li>
  <li>자바스크립트 파일들을 묶고(bundle) 축소(minify)하기</li>
  <li>자바스크립트가 코딩 규칙을 따르는지 JSHint 툴로 검사하기 <br>
  . <br>
  .</li>
  </ul>
</blockquote>

<p>태스크 러너란, task 단위로 실행되며 command line을 통해 동작하는 자바스크립트 용 빌드 툴. <br>
= 웹 개발에서 반복적으로 수행되는 작업들을 자동화해서 작업 효율을 높이는 도구</p>

<p><img src="http://cfile3.uf.tistory.com/image/2314133B55EEEA070AED25" alt="enter image description here" title=""></p>

<hr>



<h2 id="grunt-usage">Grunt Usage</h2>



<h3 id="step1-grunt-cli-설치">Step1. Grunt CLI 설치</h3>

<blockquote>
  <p><strong>Note: </strong> npm(Node Package Modules)이 설치되어 있지 않다면 먼저 설치한다.  <br>
  <a href="https://nodejs.org/en/download/">https://nodejs.org/en/download/</a></p>
</blockquote>

<p>Grunt CLI의 역할은 그저 Gruntfile이라는 파일이 있는 위치에 설치된 Grunt를 찾아서 실행하는 것이다. <br>
cmd를 열고 다음과 같이 입력한다.</p>

<pre><code>$ npm install -g grunt-cli
</code></pre>

<hr>



<h3 id="step2-프로젝트의-루트-디렉토리에-두-개의-필수-파일-생성">Step2. 프로젝트의 루트 디렉토리에 두 개의 필수 파일 생성</h3>

<p>프로젝트 구조 sample</p>

<p><img src="https://i2.wp.com/csharpcorner.mindcrackerinc.netdna-cdn.com/article/getting-started-with-grunt-task-runner/Images/Folder.jpg" alt="enter image description here" title=""></p>



<h5 id="a-packagejson"><strong>A) package.json</strong></h5>

<p>npm module로서 프로젝트를 관리하는데 필요한 메타데이터를 쌓기 위한 파일.  <br>
 그런트와 그런트 플러그인들이 <em>devDependencies</em>에 리스트업 된다.</p>

<pre><code>$ npm init
</code></pre>

<p><img src="http://marcinjuraszek.com/wp-content/uploads/2014/11/PackageJson.png" alt="enter image description here" title=""></p>

<blockquote>
  <p><strong>Note:</strong></p>
  
  <ul>
  <li><em>name</em>과 <em>version</em>은 필수 항목. 나머지는 사용자가 추가 삭제가 가능.</li>
  <li><em>name</em>은 점( . )이나 밑줄( _ )로 시작할 수 없다.</li>
  <li><em>name</em>은 대문자를 포함해서는 안된다.</li>
  </ul>
</blockquote>



<h5 id="b-gruntfilejs"><strong>B) Gruntfile.js</strong></h5>

<p>package.json의 정보를 이용하고 그런트 설정을 담당하는 파일로 자바스크립트 파일 혹은 커피스크립트 파일.</p>

<p><img src="http://www.techjira.com/node/grunt/grunt_structure.png" alt="enter image description here" title=""></p>

<hr>



<h3 id="step3-gruntgrunt-plugins-설치">Step3. Grunt/Grunt Plugins 설치</h3>



<h5 id="그런트-설치"><strong>그런트 설치</strong></h5>

<pre><code>$ npm install grunt --save-dev
</code></pre>



<h5 id="그런트-플러그인-설치-example"><strong>그런트 플러그인 설치 example</strong></h5>

<pre><code>$ npm install grunt-contrib-jshint --save-dev
</code></pre>

<blockquote>
  <p><strong>Note:</strong></p>
  
  <ul>
  <li><a href="https://github.com/gruntjs/grunt-contrib-csslint">grunt-contrib-csslint</a>: CSS lint</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-cssmin">grunt-contrib-cssmin</a>: CSS minify </li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-imagemin">grunt-contrib-imagemin</a>: 이미지 최적화</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-watch">grunt-contrib-watch</a>: 파일 실시간 감시 및 재생산</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-connect">grunt-contrib-connect</a>: 웹서버를 띄운다</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-uglify">grunt-contrib-uglify</a>: file minify</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-concat">grunt-contrib-concat</a>: 파일 병합</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-clean">grunt-contrib-clean</a>: 폴더 및 파일 삭제</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-copy">grunt-contrib-copy</a>: 파일 복사</li>
  <li><a href="https://github.com/gruntjs/grunt-contrib-jshint">grunt-contrib-jshint</a>: Javascript 오류 검사</li>
  <li><a href="https://github.com/sindresorhus/jshint-stylish">jshint-stylish</a>: jshint를 보기좋게 꾸며줌</li>
  <li><a href="https://github.com/alanshaw/grunt-include-replace">grunt-include-replace</a>: grunt-include를 대신하여 인클루드를 사용하고, 문자열 변경이 가능</li>
  <li><a href="https://www.npmjs.com/package/grunt-htmlhint">grunt-htmlhint</a>: html 오류 검사</li>
  <li><a href="https://www.npmjs.com/package/grunt-jsbeautifier">jgrunt-sbeautifier</a>: 코드 정리</li>
  <li><a href="https://www.npmjs.com/package/grunt-sass">grunt-sass</a> : Sass 컴파일</li>
  <li><a href="https://github.com/tschaub/grunt-newer">grunt-newer</a>: 파일이 수정된 부분만 컴파일 되도록 함</li>
  <li><a href="https://github.com/sindresorhus/grunt-concurrent">grunt-concurrent</a>: task를 병렬로 실행</li>
  <li><a href="https://github.com/nDmitry/grunt-autoprefixer">grunt-autoprefixer</a>: autoprefixer</li>
  <li><a href="https://www.npmjs.com/package/jit-grunt">jit-grunt</a>: 자동으로 그런트 플러그인 로드</li>
  <li><a href="https://www.npmjs.com/package/time-grunt">time-grunt</a>: 최적화를 수행하기 위해 그런트 작업의 경과된 시간을 표시</li>
  </ul>
</blockquote>

<hr>



<h3 id="step4-gruntfilejs-작성">Step4. Gruntfile.js 작성</h3>



<pre class="prettyprint"><code class=" hljs javascript">module.exports = <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(grunt)</span> {</span>
  <span class="hljs-comment">// 가) 프로젝트 환경설정</span>
  grunt.initConfig({
    pkg: grunt.file.readJSON(<span class="hljs-string">'package.json'</span>),
    <span class="hljs-comment">// task 설정</span>
  });
  <span class="hljs-comment">// 나) 플러그인 로드</span>
  <span class="hljs-comment">// 다) task 실행</span>
}</code></pre>



<h5 id="a-task-설정"><strong>A) task 설정</strong></h5>

<p><img src="http://postfiles9.naver.net/MjAxNjEyMDdfNjgg/MDAxNDgxMDk5NTk4Nzgz.JAU11GSfGp4KyIq0c7bRmNrG45jhd3Q_k_KarKDFkmUg.cZb4jxyV8fqX9IYSf7UigCnwjobrBzz-zoS4Hd1CJEwg.PNG.yoplle/target.png?type=w2" alt="enter image description here" title=""></p>

<blockquote>
  <ol>
  <li><strong>dist:</strong> task의 이름. 사용자 변경이 가능. 일반적으로 <em>distribute</em>의 약자로 <em>dist</em>를 많이 사용.</li>
  <li><strong>cwd:</strong> <em>current working directory.</em> 소스폴더의 경로 </li>
  <li><strong>src:</strong> 소스폴더의 파일형식.  (<a href="http://gruntjs.com/configuring-tasks#globbing-patterns">globbing patterns 사용 방법 참고</a>)</li>
  <li><strong>dest:</strong> 목적지(배포) 폴더. </li>
  </ol>
</blockquote>



<h5 id="b-플러그인-로드"><strong>B) 플러그인 로드</strong></h5>



<pre class="prettyprint"><code class=" hljs bash">grunt.loadNpmTasks(<span class="hljs-string">'grunt-autoprefixer'</span>);
grunt.loadNpmTasks(<span class="hljs-string">'grunt-contrib-cssmin'</span>);
.
.</code></pre>

<p><em>PLUGINNAME</em>에 설치된 플러그인명을 입력한다. <br>
load-grunt-tasks 플러그인이나, jit-grunt 플러그인을 설치하면 여러개의 그런트 플러그인을 자동으로 로드할 수 있다.</p>



<h5 id="c-task-등록"><strong>C) task 등록</strong></h5>



<pre class="prettyprint"><code class=" hljs avrasm">grunt<span class="hljs-preprocessor">.task</span><span class="hljs-preprocessor">.registerTask</span>(TASKNAME, [.<span class="hljs-preprocessor">.tasks</span>..])</code></pre>

<p><em>TASKNAME</em>은 작업명에 대한 별칭이다. 작업명은 하나가 될 수도 있고 여러 개가 될 수도 있다. <br>
그런트는 기본으로 default 작업명을 지원한다.</p>



<pre class="prettyprint"><code class=" hljs bash">grunt.registerTask(<span class="hljs-string">'default'</span>, [
    <span class="hljs-string">'concat_css'</span>, 
    <span class="hljs-string">'cssmin'</span>
]);</code></pre>

<hr>



<h3 id="step5-실행하기">Step5. 실행하기</h3>

<p>처음 실행 시(빌드를 하고 감시를 할 때)</p>

<pre><code>$ grunt serv
</code></pre>

<p>2번째 이후(빌드 후 감시대상이 있을 때 default task를 생략)</p>

<pre><code>$ grunt serve:dist
</code></pre>

<hr>



<h2 id="grunt-vs-gulp">Grunt VS Gulp</h2>

<p><img src="https://lh5.googleusercontent.com/sJslIcCSh-m6MaqGaIfMaECtlFQKmQa8Nb5LyLH9HhUxFE-64TlBlmdmq551WXY1wJa9pcGwQd8aXG4fFM2fWy-0R3kqPmCZO09Y0HJ3HfRxp0VHOkpX7q-MkZ2sc3h91nFG5tw" alt="enter image description here" title=""></p>

<blockquote>
  <p><strong>Note:</strong></p>
  
  <ul>
  <li>task 설정 방식이 다르다.  <br>
  Grunt is configuration-based. Gulp is stream-based.</li>
  <li>task 실행 방식이 다르다.  <br>
  Grunt runs the processes you want to execute in a sequential manner. Gulp tries to run them with maximum concurrency, meaning it will try to execute processes in parallel if possible.</li>
  </ul>
</blockquote>



<h4 id="task-설정-방식">task 설정 방식</h4>

<p>A) Grunt</p>



<pre class="prettyprint"><code class=" hljs javascript">module.exports = <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(grunt)</span> {</span>
  <span class="hljs-comment">// Report the task-execution time in the command line</span>
  <span class="hljs-built_in">require</span>(<span class="hljs-string">'time-grunt'</span>)(grunt);
  <span class="hljs-comment">// Task configuration</span>
  grunt.initConfig({
    pkg: grunt.file.readJSON(<span class="hljs-string">'package.json'</span>),
    <span class="hljs-comment">// Combine all CSS files found inside the src directory</span>
    concat_css: {
      dist: {
        src: [<span class="hljs-string">'src/*.css'</span>],
        dest: <span class="hljs-string">'css/styles.css'</span>
      }
    },
    <span class="hljs-comment">// Minify the stylesheet</span>
    cssmin: {
      target: {
        <span class="hljs-comment">// Write the minified file in the css directory</span>
        files: [{
          <span class="hljs-string">'css/styles.min.css'</span>: [<span class="hljs-string">'css/styles.css'</span>]
        }]
      }
    }
  });
  <span class="hljs-comment">// 플러그인 로드</span>
  grunt.loadNpmTasks(<span class="hljs-string">'grunt-concat-css'</span>);
  grunt.loadNpmTasks(<span class="hljs-string">'grunt-contrib-cssmin'</span>);
  <span class="hljs-comment">// task 등록</span>
  grunt.registerTask(<span class="hljs-string">'default'</span>, [<span class="hljs-string">'concat_css'</span>, <span class="hljs-string">'cssmin'</span>]);
}</code></pre>

<p>B) Gulp</p>



<pre class="prettyprint"><code class=" hljs javascript"><span class="hljs-comment">// Load the plugins</span>
<span class="hljs-keyword">var</span> gulp = <span class="hljs-built_in">require</span>(<span class="hljs-string">'gulp'</span>);
<span class="hljs-keyword">var</span> concatenate = <span class="hljs-built_in">require</span>(<span class="hljs-string">'gulp-concat-css'</span>);
<span class="hljs-keyword">var</span> minify = <span class="hljs-built_in">require</span>(<span class="hljs-string">'gulp-cssmin'</span>);
<span class="hljs-keyword">var</span> duration = <span class="hljs-built_in">require</span>(<span class="hljs-string">'gulp-duration'</span>);
<span class="hljs-comment">// Task configuration</span>
gulp.task(<span class="hljs-string">'default'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">()</span> {</span>
  gulp.src(<span class="hljs-string">'src/*.css'</span>)
  <span class="hljs-comment">// Combine all CSS files found inside the src directory</span>
  .pipe(concatenate(<span class="hljs-string">'styles.min.css'</span>))
  <span class="hljs-comment">// Minify the stylesheet</span>
  .pipe(minify())
  <span class="hljs-comment">// Report the task-execution time in the command line</span>
  .pipe(duration(<span class="hljs-string">'Execution Time: '</span>))
  <span class="hljs-comment">// Write the minified file in the css directory</span>
  .pipe(gulp.dest(<span class="hljs-string">'css/'</span>));
});
<span class="hljs-comment">// Use `gulp` command to run the task</span></code></pre>



<h4 id="컴파일-속도">컴파일 속도</h4>

<p>A) javascript uglify</p>

<p><img src="http://tech.tmw.co.uk/img/blog/kickoff-gulp-test/compare-sass.gif" alt="enter image description here" title=""></p>

<p>B) Sass</p>

<p><img src="http://tech.tmw.co.uk/img/blog/kickoff-gulp-test/compare-js.gif" alt="enter image description here" title=""></p>



<h4 id="npm-stat">npm stat</h4>

<p><a href="https://npm-stat.com/charts.html?package=grunt&amp;package=gulp&amp;from=2013-01-01&amp;to=2016-10-28">https://npm-stat.com/charts.html?package=grunt&amp;package=gulp&amp;from=2013-01-01&amp;to=2016-10-28</a></p>

<p><img src="http://postfiles1.naver.net/MjAxNjEyMDdfMjYx/MDAxNDgxMDk5NzQ4NjY2.3TzO_PEMY-U64HQzHKtgdbUPmUPUxUMFOS_6rtsov7og.OdPlgAVb3x-vxYRQcdjo22AiP54yY11WJxU90UNa7UAg.PNG.yoplle/%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C.png?type=w2" alt="enter image description here" title=""></p>

<hr>



<h2 id="pros-and-cons">Pros. and Cons.</h2>



<h4 id="pros">Pros.</h4>

<ul>
<li>개발속도가 빨라진다. <em>speed-up development process</em> </li>
<li>코드품질이 향상된다. <em>improvement of code quality</em></li>
<li>중복코드를 현저히 줄여준다. <em>significantly reduced code duplication</em> </li>
<li>실시간 프로그래밍이 가능하다. <em>possibility to program in real time</em></li>
</ul>



<h4 id="cons">Cons.</h4>

<ul>
<li>진입 장벽이 높다. <em>high barrier to entry into the environment</em></li>
<li>자바스크립트 피로도. <em>javascript fatigue</em></li>
<li>모듈 설정 방법 선택의 폭이 넓다. <em>wide choice of module configuration methods</em></li>
<li>FAQ 자료가 부족하다. <em>lack of FAQ resources</em></li>
</ul>

<hr>



<h2 id="references">References</h2>

<ul>
<li><a href="http://gruntjs.com/">http://gruntjs.com/</a></li>
<li><a href="http://blog.jakeymvc.com/task-runner/">http://blog.jakeymvc.com/task-runner/</a></li>
<li><a href="http://frontendinsights.com/modern-front-end-development-technology-stack/">http://frontendinsights.com/modern-front-end-development-technology-stack/</a></li>
<li><a href="http://programmingsummaries.tistory.com/377">http://programmingsummaries.tistory.com/377</a></li>
<li><a href="http://sixrevisions.com/web-development/grunt-vs-gulp/">http://sixrevisions.com/web-development/grunt-vs-gulp/</a></li>
<li><a href="http://tech.tmw.co.uk/2014/01/speedtesting-gulp-and-grunt/">http://tech.tmw.co.uk/2014/01/speedtesting-gulp-and-grunt/</a></li>
<li><a href="https://www.keithcirkel.co.uk/why-we-should-stop-using-grunt/">https://www.keithcirkel.co.uk/why-we-should-stop-using-grunt/</a></li>
<li><a href="https://anadea.info/blog/modern-front-end-pros-and-cons">https://anadea.info/blog/modern-front-end-pros-and-cons</a></li>
<li><a href="https://blog.outsider.ne.kr/1181">https://blog.outsider.ne.kr/1181</a></li>
</ul></div></body>
</html>