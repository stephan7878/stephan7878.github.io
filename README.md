# [stephan7878.github.io](https://stephan7878.github.io)

This is the repository for my blog, created with Jekyll and hosted on GitHub Pages.

## Local Development

### Installation

If you are using an Ubuntu environment, follow the instruction below, otherwise check out the [Jekyll Installation Guides](https://jekyllrb.com/docs/installation/#guides) for your operating system.

- Install prerequisites:

```shell
sudo apt-get install ruby-full build-essential zlib1g-dev
```

- Setup environment:

```shell
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

- Install software:

```shell
gem install jekyll bundler
```

### Build

- Clone this repository.

```shell
git clone https://github.com/stephan7878/stephan7878.github.io.git
```

- Navigate to the root directory of the repository.

```shell
cd stephan7878.github.io/
```

- Install dependencies.

```shell
bundle install
```

- Build and serve the site.

```shell
bundle exec jekyll serve
```

## Useful Links

- [GitHub Pages](https://pages.github.com/)
- [Jekyll Quickstart](https://jekyllrb.com/docs/)
- [Build A Portfolio With A Blog Using GitHub Pages](https://simondosda.github.io/posts/2021-09-13-blog-github-pages-1-introduction.html)
