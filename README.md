# How to write when you use another computer?

0、Install [Git](<https://git-scm.com/downloads>) and [Node. js](<https://nodejs.org/zh-cn/download/>)

1、git clone master branch of this repository

2、Create a new local branch, and switch to remote branch backup: `git checkout -b backup origin/backup`（Notice: at this point, you are on the local `backup branch`）

3、Install hexo using the npm command: try `npm install -g hexo-cli` or `npm install -g hexo` or `npm install hexo --save` 

4、Writing

5、`hexo g` --> `hexo d`, complete.

Finally, use the command `git push` to upload files for backup to remote `backup branch`。

Notice, this backup branch mainly backed up following folders and files：

``` xml
source/ 
scaffolds/
theme/
README.md
_config.yml
package-lock.json
package.json
```

`.gitignore` file contains the following contents: 

``` xml
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
```

