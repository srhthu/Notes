total package: 1755

single node: 19
top node: 70
bottom node: 392

不准，图里有环，例如libfl-dev和flex

从顶部遍历。对所有底部包，根据其最短遍历路径找到顶部包，更新顶部包的最长路径长度：
> - ('code', 31),
> - ('aspell-en', 15),
> - ('ffmpeg', 10),
> - ('cuda-demo-suite-11-4', 10),
> - ('ubuntu-desktop', 9),
> - ('fcitx-config-gtk', 9
> - ('openjdk-8-jre-headless', 8),
> - ('google-chrome-stable', 8),
> - ('linux-generic-hwe-20.04', 6),
> - ('gnome-user-docs-zh-hans', 6),