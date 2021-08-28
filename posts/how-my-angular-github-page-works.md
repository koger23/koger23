I start my first post with presenting how this page works under the hood but on high level, how I store the posts and the content of the other pages and how they are being rendered.

## GitHub page
As you might know you can create a [GitHub page](https://pages.github.com/) for yourself if you create a public repository with the name `your-github-username.github.io`. You can host your own website on GitHub this way.

This site is a [SPA (Single-page application)](https://en.wikipedia.org/wiki/Single-page_application) made with [Angular 12](https://angular.io) framework which is a TypeScript-based free and open-source web application framework. A SPA interacts with the user by dynamically rewriting the current web page with new data from the web server.

## The web server
Since this is a GitHub page and my idea was to share some of my selected projects found on GitHub, I decided to use my public GitHub repositories as source.

## The build-up of pages
There are 4 types of pages: home, projects, posts and about. Projects and posts are lists of those. All of these are made as components in Angular:
```
├── about
├── home
├── posts
│   ├── post
│   └── posts-list-item
└── projects
    ├── project
    └── project-list-item

```
Posts and projects are very similar, but they have been created separate components for later flexibility.

## Data Sources
The data sources are my public repositories on GitHub. This sites loads raw markdown files as contents. These must be converted to HTML for rendering, which is done by a pipe `markedown`. All content are available on `https://raw.githubusercontent.com/{username}/{reponame}/{branchname}/{filename}`, where the services collect the markodwn files from.

### Configurations
Before we go further, we need to know how and what we store as configuration settings.
Since the website uses GitHub as data server, the settings are stored in a `.ini` structured file named `koger23.github.io.cfg` in 'koger23' repostiory. It has a `[DEFAULT]` section, which stores the most important basic informations as options like the list of posts or the list of project repositories:
```
[DEFAULT]
projects = csipesz-jelzo,PyImageViewer,koger23.github.io
posts = how-my-angular-github-page-works
```
The home and the about pages are also stored as markdown files, but they are independent components.

### Projects
Projects must be public repositories to make possible loading the content for them. This site loads the `README.md` of the projects, then the image references are replaced with the full URL instead of relative path.

### Posts
Posts are stored on 'koger23' repository also as markdown files under folder 'posts'. Images are stored in separate folder 'img'.

## Summary
I summarized how the content of the pages are stored, where their configuraions are stored and how they are loaded. All from public GitHub repositories.