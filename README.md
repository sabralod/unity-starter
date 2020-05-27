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