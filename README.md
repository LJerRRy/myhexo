# my hexo
echo "# myhexo" >> README.md<br>
git init<br>
git add README.md<br>
git commit -m "first commit"<br>
git remote add origin https://github.com/LJerRRy/myhexo.git<br>
git push -u origin master<br>

##clone
everytime you should excute below codes:<br>
cd myhexo<br>
npm install hexo<br>
npm install hexo-server --save<br>
npm install hexo-renderer-ejs --save<br>
npm install hexo-renderer-stylus --save<br>
npm install hexo-renderer-marked --save<br>
npm install<br>

##deploy
npm install hexo-deployer-git --save<br>