# empty-jekyll-site-tailwindcss

## development environment

- Linux

- [git]

  ```shell
  sudo apt install git
  git -v
  ```

- [Ruby] (and [RubyGems])

  ```shell
  sudo apt install ruby
  ruby -v
  gem -v
  ```

  Maybe gem source have to be changed.

  ```shell
  gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
  gem sources -l
  ```

- [Bundler]

  ```shell
  gem install bundler
  bundle -v
  ```

  Maybe bundler source have to be changed as well.

  ```shell
  bundle config mirror.https://rubygems.org https://gems.ruby-china.com
  bundle config
  bundle config mirror.https://rubygems.org
  ```

- [Jekyll]

  ```shell
  gem install jekyll
  jekyll -v
  ```

## Start a new [Jekyll] project

  ```shell
  jekyll new <YOUR PROJECT NAME> --blank
  ```

## Set up git

  ```shell
  cd <YOUR PROJECT NAME>
  git init
  ```
  
  Maybe rename the branch.

  `git branch -m <OLD BRANCH NAME> <NEW BRANCH NAME>`

  Create a file named `.gitignore` and paste the following in it:

  ```
  _site/
  .sass-cache/
  .jekyll-cache/
  .jekyll-metadata
  node_modules
  ```

## Install [Ruby] gems

  Create a `Gemfile` which is a list of gems used by your site. Add it to the root directory with the following content:

  ```
  source 'https://rubygems.org'

  gem 'jekyll'
  gem 'webrick'
  ```

  Now install those gems by [Bundler].

  `bundle`

## Build the [Jekyll] site

  `bundle exec jekyll serve`

  Open <localhost:4000> in your browser. If you see something like this.

  ![readytogo](assets/pics/readytogo.png)

## Add [PostCSS] and [Tailwind]

  Paste `gem jekyll-postcss-v2` into `Gemfile` and install the gem.

  `bundle`

  Open the `_config.yml` file and add the following lines at the end.

  ```
  plugins:
    - jekyll-postcss-v2
  ```

  Now create a `postcss.config.js` file in the root directory and add [Tailwind] to your [PostCSS] configuration.

  ```
  module.exports = {
    plugins: [
      require('tailwindcss'),
      require('autoprefixer'),
      ...(process.env.JEKYLL_ENV == 'production'
        ? [require('cssnano')({ preset: 'default' })]
        : [])
    ]
  }
  ```

  Install those packages.

  `npm install -D postcss postcss-cli tailwindcss autoprefixer cssnano`

## Configure [Taiwind]

  Create a `tailwind.config.js` file in the root directory with the following contents. You can use `npx tailwindcss init` to create the file.

  ```
  module.exports = {
    content: [
      './_drafts/**/*.html',
      './_includes/**/*.html',
      './_layouts/**/*.html',
      './_posts/*.md',
      './*.md',
      './*.html',
    ],
    theme: {
      theme: {
        extend: {},
      },
    },
    plugins: []
  }
  ```

  Rename `assets/css/main.scss` to `assets/css/main.css` and put the following in it.

  ```
  ---
  ---

  @tailwind base;
  @tailwind components;
  @tailwind utilities;
  ```

  Then remove the `_sass` directory.

## Start using [Tailwind] in your HTML

  Open `_layouts/default.html` and add `class="text-red-500"` attribute to the `<body>` tag.

  Rebuild the [Jekyll] site. You should see this.

  ![readytogo](assets/pics/readytogo-red.png)

## Publish to [Github] (optional)

  Add files to the staging area and commit your changes.

  ```shell
  git add .
  git commit -m 'Your commit message'
  ```
  Create a [Github] repository.
  
  - Go to GitHub.com and sign in to your account.

  - Click on the "+" button in the top right corner and select "New repository."

  - Give your repository a name and description.

  - Choose whether you want the repository to be public or private.

  - Click "Create repository."

  Connect the local repository to [Github].

  `git remote add origin https://github.com/<your_username>/<your_repository_name>.git`

  Push your local changes to [Github].

  `git push origin main`

You'r made it.

## Usefull links

- [Starting a blank Jekyll site with Tailwind CSS in 2022](https://mzrn.sh/2022/04/09/starting-a-blank-jekyll-site-with-tailwind-css-in-2022)

- [Installation - Jekyll](https://jekyllrb.com/docs/installation)

- [Creating a new repository - Github](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository)

- [bglw/jekyll-postcss-v2](https://github.com/bglw/jekyll-postcss-v2)

- [Get started with Tailwind CSS](https://tailwindcss.com/docs/installation/using-postcss)

## Related repositories

- [longavailable/empty-jekyll-site](https://github.com/longavailable/empty-jekyll-site)

<!--links-->
[Ruby]:https://www.ruby-lang.org/en/documentation/installation
[RubyGems]:https://github.com/rubygems/rubygems?tab=readme-ov-file#installation
[Bundler]:https://bundler.io
[Jekyll]:https://jekyllrb.com
[git]:https://git-scm.com
[github]:https://github.com
[Tailwind]:https://tailwindcss.com
[PostCSS]:https://postcss.org
