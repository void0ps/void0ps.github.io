Hugo project structure  Hugo 项目结构
Before leaping into it, first a quick note about Hugo project structure and best practices for managing your content and theme customisations.
在深入探讨之前，首先快速了解一下 Hugo 项目结构以及管理内容和主题自定义的最佳实践。

In summary: Never directly edit the theme files. Only make customisations in your Hugo project’s sub-directories, not in the themes directory itself.
总之： 切勿直接编辑主题文件。只能在 Hugo 项目的子目录中进行自定义，而不要在主题目录本身中进行编辑。
Blowfish is built to take advantage of all the standard Hugo practices. It is designed to allow all aspects of the theme to be customised and overridden without changing any of the core theme files. This allows for a seamless upgrade experience while giving you total control over the look and feel of your website.
Blowfish 主题的设计充分利用了 Hugo 的所有标准实践。它允许对主题的各个方面进行自定义和覆盖，而无需更改任何核心主题文件。这既能带来无缝的升级体验，又能让您完全掌控网站的外观和风格。

In order to achieve this, you should never manually adjust any of the theme files directly. Whether you install using Hugo modules, as a git submodule or manually include the theme in your themes/ directory, you should always leave these files intact.
为了达到这个目的，你绝对不应该直接手动修改任何主题文件。无论你是使用 Hugo 模块安装、作为 Git 子模块安装，还是手动将主题添加到 themes/ 目录中，都应该始终保持这些文件不变。

The correct way to adjust any theme behaviour is by overriding files using Hugo’s powerful file lookup order. In summary, the lookup order ensures any files you include in your project directory will automatically take precedence over any theme files.
调整主题行为的正确方法是使用 Hugo 强大的文件查找顺序功能来覆盖文件。简而言之，查找顺序功能确保您包含在项目目录中的任何文件都会自动优先于任何主题文件。

For example, if you wanted to override the main article template in Blowfish, you can simply create your own layouts/_default/single.html file and place it in the root of your project. This file will then override the single.html from the theme without ever changing the theme itself. This works for any theme files - HTML templates, partials, shortcodes, config files, data, assets, etc.
例如，如果您想在 Blowfish 主题中覆盖主文章模板，只需创建您自己的 layouts/_default/single.html 文件并将其放置在项目根目录即可。这样，该文件将覆盖主题中的 single.html 文件，而无需更改主题本身。此方法适用于任何主题文件——HTML 模板、局部视图、短代码、配置文件、数据、资源等等。

As long as you follow this simple practice, you will always be able to update the theme (or test different theme versions) without worrying that you will lose any of your custom changes.
只要你遵循这个简单的做法，你就可以随时更新主题（或测试不同的主题版本），而不用担心丢失任何自定义更改。

Change image optimization settings
更改图像优化设置
Hugo has various builtin methods to resize, crop and optimize images.
Hugo 内置了多种调整图像大小、裁剪和优化图像的方法。

As an example - in layouts/partials/article-link/card.html, you have the following code:
例如，在 layouts/partials/article-link/card.html 中，您有以下代码：

{{ with .Resize "600x" }}
<div class="w-full thumbnail_card nozoom" style="background-image:url({{ .RelPermalink }});"></div>
{{ end }}
The default behavior of Hugo here is to resize the image to 600px keeping the ratio.
Hugo 的默认行为是将图像大小调整为 600 像素，并保持宽高比。

It is worth noting here that default image configurations such as anchor point can also be set in your site configuration as well as in the template itself.
值得注意的是，除了模板本身之外，还可以在网站配置中设置默认图像配置（例如锚点） 。

See the Hugo docs on image processing for more info.
有关图像处理的更多信息，请参阅 Hugo 文档 。

Colour schemes  配色方案
Blowfish ships with a number of colour schemes out of the box. To change the basic colour scheme, you can set the colorScheme theme parameter. Refer to the Getting Started section to learn more about the built-in schemes.
Blowfish 内置多种配色方案。要更改基本配色方案，您可以设置 colorScheme 主题参数。有关内置方案的更多信息，请参阅“ 入门指南 ”部分。

In addition to the default schemes, you can also create your own and re-style the entire website to your liking. Schemes are created by by placing a <scheme-name>.css file in the assets/css/schemes/ folder. Once the file is created, simply refer to it by name in the theme configuration.
除了默认方案外，您还可以创建自己的方案，并根据喜好重新设计整个网站。创建方案的方法是将一个 <scheme-name>.css 的文件放置在 assets/css/schemes/ 文件夹中。文件创建完成后，只需在主题配置中按名称引用即可。

Note: generating these files manually can be hard, I’ve built a nodejs terminal tool to help with that, Fugu. In a nutshell, you pass the main three hex values of your color palette and the program will output a css file that can be imported directly into Blowfish.
注意： 手动生成这些文件可能比较麻烦，所以我开发了一个名为 Fugu 的 nodejs 终端工具来辅助完成这项工作。简而言之，你只需传入调色板中的三个主要 hex 颜色值，程序就会输出一个可以直接导入 Blowfish 的 CSS 文件。
Blowfish defines a three-colour palette that is used throughout the theme. The three colours are defined as neutral, primary and secondary variants, each containing ten shades of colour.
Blowfish 定义了一个贯穿整个主题的三色调色板。这三种颜色分别是 neutral 、 primary 和 secondary 色，每种颜色都包含十种色调。

Due to the way Tailwind CSS 3.0 calculates colour values with opacity, the colours specified in the scheme need to conform to a particular format by providing the red, green and blue colour values.
由于 Tailwind CSS 3.0 计算颜色值和不透明度的方式，方案中指定的颜色需要符合特定的格式， 即提供红色、绿色和蓝色颜色值。

:root {
  --color-primary-500: 139, 92, 246;
}
This example defines a CSS variable for the primary-500 colour with a red value of 139, green value of 92 and blue value of 246.
此示例定义了一个 CSS 变量，用于表示 primary-500 ，红色值为 139 ，绿色值为 92 ，蓝色值为 246 。

Use one of the existing theme stylesheets as a template. You are free to define your own colours, but for some inspiration, check out the official Tailwind colour palette reference.
使用现有的主题样式表作为模板。您可以自由定义自己的颜色，但为了获得一些灵感，请查看官方的 Tailwind 调色板参考 。

Overriding the stylesheet
覆盖样式表
Sometimes you need to add a custom style to style your own HTML elements. Blowfish provides for this scenario by allowing you to override the default styles in your own CSS stylesheet. Simply create a custom.css file in your project’s assets/css/ folder.
有时您需要添加自定义样式来设置 HTML 元素的样式。Blowfish 允许您在自己的 CSS 样式表中覆盖默认样式，从而满足这一需求。只需在项目的 assets/css/ 文件夹中创建一个 custom.css 文件即可。

The custom.css file will be minified by Hugo and loaded automatically after all the other theme styles which means anything in your custom file will take precedence over the defaults.
custom.css 文件将由 Hugo 进行压缩，并在所有其他主题样式之后自动加载，这意味着您自定义文件中的任何内容都将优先于默认值。

Using additional fonts  使用其他字体
Blowfish allows you to easily change the font for your site. After creating a custom.css file in your project’s assets/css/ folder, place you font file inside a fonts folder within the static root folder.
Blowfish 允许您轻松更改网站字体。在项目 assets/css/ 文件夹中创建 custom.css 文件后，将字体文件放置在 static 根文件夹下的 fonts 文件夹中。

.
├── assets
│   └── css
│       └── custom.css
...
└─── static
    └── fonts
        └─── font.ttf
This makes the font available to the website. Now, the font can just import it in your custom.css and replaced wherever you see fit. The example below shows what replacing the font for the entire html would look like.
这样，网站就可以使用该字体了。现在，您只需将字体导入到 custom.css 文件中，并根据需要进行替换即可。下面的示例展示了替换整个 html 中的字体后的效果。

@font-face {
    font-family: font;
    src: url('/fonts/font.ttf');
}

html {
    font-family: font;
}
Adjusting the font size  调整字体大小
Changing the font size of your website is one example of overriding the default stylesheet. Blowfish makes this simple as it uses scaled font sizes throughout the theme which are derived from the base HTML font size. By default, Tailwind sets the default size to 12pt, but it can be changed to whatever value you prefer.
更改网站字体大小是覆盖默认样式表的一个例子。Blowfish 主题简化了这一操作，因为它在整个主题中使用了基于 HTML 基础字体大小的缩放字体大小。默认情况下，Tailwind 将默认字体大小设置为 12pt ，但您可以将其更改为您喜欢的任何值。

Create a custom.css file using the instructions above and add the following CSS declaration:
按照上述说明创建 custom.css 文件，并添加以下 CSS 声明：

/* Increase the default font size */
html {
  font-size: 13pt;
}
Simply by changing this one value, all the font sizes on your website will be adjusted to match this new size. Therefore, to increase the overall font sizes used, make the value greater than 12pt. Similarly, to decrease the font sizes, make the value less than 12pt.
只需更改此值，网站上所有字体大小都会调整为与新大小一致。因此，要增大字体大小，请将该值设置为大于 12pt 。同样，要减小字体大小，请将该值设置为小于 12pt 。

Building the theme CSS from source
从源代码构建主题 CSS
If you’d like to make a major change, you can take advantage of Tailwind CSS’s JIT compiler and rebuild the entire theme CSS from scratch. This is useful if you want to adjust the Tailwind configuration or add extra Tailwind classes to the main stylesheet.
如果您想进行重大更改，可以利用 Tailwind CSS 的 JIT 编译器从头开始重新构建整个主题 CSS。如果您想调整 Tailwind 配置或向主样式表添加额外的 Tailwind 类，这将非常有用。

Note: Building the theme manually is intended for advanced users.
注意： 手动构建主题仅供高级用户使用。
Let’s step through how building the Tailwind CSS works.
让我们逐步了解一下 Tailwind CSS 的构建过程。

Tailwind configuration  顺风配置
In order to generate a CSS file that only contains the Tailwind classes that are actually being used the JIT compiler needs to scan through all the HTML templates and Markdown content files to check which styles are present in the markup. The compiler does this by looking at the tailwind.config.js file which is included in the root of the theme directory:
为了生成仅包含实际使用的 Tailwind 类的 CSS 文件，JIT 编译器需要扫描所有 HTML 模板和 Markdown 内容文件，以检查标记中存在的样式。编译器通过查看主题目录根目录下的 tailwind.config.js 文件来实现这一点：

// themes/blowfish/tailwind.config.js

module.exports = {
  content: [
    "./layouts/**/*.html",
    "./content/**/*.{html,md}",
    "./themes/blowfish/layouts/**/*.html",
    "./themes/blowfish/content/**/*.{html,md}",
  ],

  // and more...
};
This default configuration has been included with these content paths so that you can easily generate your own CSS file without needing to modify it, provided you follow a particular project structure. Namely, you have to include Blowfish in your project as a subdirectory at themes/blowfish/. This means you cannot easily use Hugo Modules to install the theme and you must go down either the git submodule (recommended) or manual install routes. The Installation docs explain how to install the theme using either of these methods.
这些内容路径中包含了默认配置，以便您无需修改​​即可轻松生成自己的 CSS 文件，前提是您遵循特定的项目结构。具体来说， 您必须将 Blowfish 作为子目录添加到项目中，路径为 themes/blowfish/ 。这意味着您无法直接使用 Hugo Modules 安装主题，而必须通过 Git 子模块（推荐）或手动安装方式进行安装。 安装文档详细说明了如何使用这两种方法安装主题。

Project structure  项目结构
In order to take advantage of the default configuration, your project should look something like this…
为了利用默认配置，您的项目应该类似于这样……

.
├── assets
│   └── css
│       └── compiled
│           └── main.css  # this is the file we will generate
├── config  # site config
│   └── _default
├── content  # site content
│   ├── _index.md
│   ├── projects
│   │   └── _index.md
│   └── blog
│       └── _index.md
├── layouts  # custom layouts for your site
│   ├── partials
│   │   └── extend-article-link/simple.html
│   ├── projects
│   │   └── list.html
│   └── shortcodes
│       └── disclaimer.html
└── themes
    └── blowfish  # git submodule or manual theme install
This example structure adds a new projects content type with its own custom layout along with a custom shortcode and extended partial. Provided the project follows this structure, all that’s required is to recompile the main.css file.
此示例结构添加了一个新的 projects 内容类型，该类型具有自定义布局、自定义短代码和扩展局部模板。如果项目遵循此结构，则只需重新编译 main.css 文件即可。

Install dependencies  安装依赖项
In order for this to work you’ll need to change into the themes/blowfish/ directory and install the project dependencies. You’ll need npm on your local machine for this step.
为了使此操作生效，您需要切换到 themes/blowfish/ 目录并安装项目依赖项。此步骤需要您的本地计算机上安装 npm 。

cd themes/blowfish
npm install
Run the Tailwind compiler
运行 Tailwind 编译器
With the dependencies installed all that’s left is to use Tailwind CLI to invoke the JIT compiler. Navigate back to the root of your Hugo project and issue the following command:
安装完依赖项后，剩下的就是使用 Tailwind CLI 调用 JIT 编译器。返回 Hugo 项目的根目录，然后执行以下命令：

cd ../..
./themes/blowfish/node_modules/@tailwindcss/cli/dist/index.mjs -c ./themes/blowfish/tailwind.config.js -i ./themes/blowfish/assets/css/main.css -o ./assets/css/compiled/main.css --jit
It’s a bit of an ugly command due to the paths involved but essentially you’re calling Tailwind CLI and passing it the location of the Tailwind config file (the one we looked at above), where to find the theme’s main.css file and then where you want the compiled CSS file to be placed (it’s going into the assets/css/compiled/ folder of your Hugo project).
由于涉及路径，这个命令有点丑陋，但本质上你是在调用 Tailwind CLI，并向它传递 Tailwind 配置文件（我们上面看到的那个）的位置、主题的 main.css 文件的位置，以及你希望编译后的 CSS 文件放置的位置（它会被放入 Hugo 项目的 assets/css/compiled/ 文件夹中）。

The config file will automatically inspect all the content and layouts in your project as well as all those in the theme and build a new CSS file that contains all the CSS required for your website. Due to the way Hugo handles file hierarchy, this file in your project will now automatically override the one that comes with the theme.
配置文件会自动检查项目和主题中的所有内容和布局，并生成一个新的 CSS 文件，其中包含网站所需的所有 CSS。由于 Hugo 处理文件层级结构的方式，项目中的这个文件现在会自动覆盖主题自带的文件。

Each time you make a change to your layouts and need new Tailwind CSS styles, you can simply re-run the command and generate the new CSS file. You can also add -w to the end of the command to run the JIT compiler in watch mode.
每次更改布局并需要新的 Tailwind CSS 样式时，只需重新运行命令即可生成新的 CSS 文件。您还可以在命令末尾添加 -w ，以监视模式运行 JIT 编译器。

Make a build script  编写构建脚本
To fully complete this solution, you can simplify this whole process by adding aliases for these commands, or do what I do and add a package.json to the root of your project which contains the necessary scripts…
为了完善这个解决方案，你可以通过为这些命令添加别名来简化整个过程，或者像我一样，在项目根目录添加一个包含必要脚本的 package.json ……

// package.json

{
  "name": "my-website",
  "version": "1.0.0",
  "description": "",
  "scripts": {
    "server": "hugo server -b http://localhost -p 8000",
    "dev": "NODE_ENV=development ./themes/blowfish/node_modules/@tailwindcss/cli/dist/index.mjs -c ./themes/blowfish/tailwind.config.js -i ./themes/blowfish/assets/css/main.css -o ./assets/css/compiled/main.css --jit -w",
    "build": "NODE_ENV=production ./themes/blowfish/node_modules/@tailwindcss/cli/dist/index.mjs -c ./themes/blowfish/tailwind.config.js -i ./themes/blowfish/assets/css/main.css -o ./assets/css/compiled/main.css --jit"
  },
  // and more...
}
Now when you want to work on designing your site, you can invoke npm run dev and the compiler will run in watch mode. When you’re ready to deploy, run npm run build and you’ll get a clean Tailwind CSS build.
现在，当您想要设计网站时，可以运行 npm run dev ，编译器将以监听模式运行。准备部署时，运行 npm run build ，即可获得一个干净的 Tailwind CSS 版本。

🙋‍♀️ If you need help, feel free to ask a question on GitHub Discussions.
🙋‍♀️ 如果您需要帮助，欢迎在 GitHub Discussions 上提问。

Documentation - This article is part of a series.