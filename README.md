# unity-starter

This project describes a way you could start with Unity game development based on a git repository.

## Using git lfs
Unity projects involving a lot of binaries, which are not working well within a text based scm like git. According to that issue git lfs (large file storage) is used to manage.
The [`.gitattributes`](./.gitattributes) file, describes patterns of binary files, that are handled by git lfs.

## Using UnityYAMLMerge
Unity ships a merge tool that can handle unity generated yaml files better. To activate UnityYAMLMerge, follow [this instructions](https://docs.unity3d.com/Manual/SmartMerge.html) or copy the [`.gitconfig_mac`](./.gitconfig_mac) example to `.gitconfig` and adjust the path to UnityYAMLMerge:
```
[merge]
tool = unityyamlmerge

[mergetool "unityyamlmerge"]
trustExitCode = false
cmd = '[Adjust this path to UnityYAMLMerge]' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
```

## Visual Studio Code integration
The unity-starter Project is configurated to use Visual Studio Code and Omnisharp.