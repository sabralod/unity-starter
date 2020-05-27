# unity-starter
This project describes a way you could start with Unity game development based on a git repository.

## Technical topics
The following section describes the technical approach to setup a Unity project with git.

### How to setup a git for a unity project
Creating a first setup with GitHub and Unity comes with a little problem. Both applications want a clean directory to create the project.
One easy approach is to:
- Create a [GitHub repository](https://github.com)
- Create a Unity project in Unity Hub on your local pc with the same name as the GitHub repository
- Clone the GitHub repository in a different directory on your local machine
- Copy the hidden `.git` directory into the Unity project directory
- Start to "git" with `git add .` and `git commit -m "Initial commit"`

### Using git lfs
Unity projects involving a lot of binaries, which are not working well within a text based scm like git. According to that issue git lfs (large file storage) is used to manage.
The [`.gitattributes`](./.gitattributes) file, describes patterns of binary files, that are handled by git lfs.

### Using UnityYAMLMerge
Unity ships a merge tool that can handle unity generated yaml files better. To activate UnityYAMLMerge, follow [this instructions](https://docs.unity3d.com/Manual/SmartMerge.html) or copy the [`.gitconfig_mac`](./.gitconfig_mac) example to `.gitconfig` and adjust the path to UnityYAMLMerge:
```
[merge]
tool = unityyamlmerge

[mergetool "unityyamlmerge"]
trustExitCode = false
cmd = '[Adjust this path to UnityYAMLMerge]' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
```

### Visual Studio Code integration
The Unity IDE comes with a Visual Studio Code integration that can be activated by following [this description](https://code.visualstudio.com/docs/other/unity).

It will create the [`./.vscode/settings.json`](./.vscode/settings.json) file with some predefined settings like:
```
"files.exclude":
    {
        "**/.DS_Store":true,
        "**/.git":true,
        // "**/.gitignore":true,
        "**/.gitmodules":true,
        "**/*.booproj":true,
        "**/*.pidb":true,
        ...
    },
    "omnisharp.useGlobalMono": "always"
```

### GitHub Actions integration
To setup a CICD pipeline, the [unity-builder](https://github.com/marketplace/actions/unity-builder?version=v1.0) GitHub action seems to be the best way for a first approach.

Ref to:
- https://github.com/marketplace/actions/unity-request-activation-file#unity---request-activation-file
- https://github.com/marketplace/actions/unity-builder?version=v1.0
- https://github.com/webbertakken/unity-actions

### Further references
- https://docs.unity3d.com/Manual/BestPracticeGuides.html
- https://thoughtbot.com/blog/how-to-git-with-unity
- https://www.reddit.com/r/gamedev/comments/6mc1az/lets_talk_about_unity_git_best_practices_and/

## Development workflow topic's
This sections describes how to setup and use a development workflow based on git.

### Branching
The git scm should have the following branches:
- `master`: Stable branch, which contains only features that are done and tests.
- `dev`: Stable branch, which is the entry point for `feature` branches. If a set of features is completed and proven as "stable", a "pull request" have to be created on GitHub for "merging" it into the `master` branch.
- `feature/xy`: Unstable branch, which contain's the work of a single feature. If the feature is done, a "pull requests" have to be created on GitHub for "merging" it into the `dev` branch.

### Making commits
A commit message should always include a reference (link) to the corresponding Issue like:
```
Brief description

Further explanation.

Fixes: https://github.com/plone/plone.app.discussion/issue/999
```

### Basic workflow
A basic workflow during development could be the following one:
```
git checkout dev
git pull
git checkout -b feature/xy
... develop the feature ...
git add .
git commit -m "Commit message; Ref: https://github.com/link/to/issue/1"
git push --set-upstream origin feature/xy
git checkout dev
git pull
git checkout feature/xy
git merge dev
... resolve merge conflicts ...
git push
... create pull request ...
```

### Further references
- https://docs.plone.org/develop/coredev/docs/git.html#making-commits
- https://www.atlassian.com/git/tutorials/comparing-workflows

## Project management topic's
A basic approach could be, to use the provided GitHub functionalities.

### Issues
- https://github.com/sabralod/unity-starter/issues

### Milestones
- https://github.com/sabralod/unity-starter/milestones

### Project board
- https://github.com/sabralod/unity-starter/projects/1