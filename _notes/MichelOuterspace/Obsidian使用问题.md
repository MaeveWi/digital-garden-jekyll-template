1. ✔️ 如何使用自定义的文字链接ob页面：[[✨导览✨|自定义的名字到导览页面]]
2. 只要文章中包含某个页面的名字，就算没有使用双链，Netlify发布后关系图中也会产生链接？
3. ⭕如何插入图片：
	1. 修改插入附件的默认位置：setting- files&links - default loaction for new attachments，选择in the folder specified below, 选择一个文件夹
	2. 有两个图片插入方式，ob官方推荐方式![[]]，或者html模式，展示问题：
		1. 官方方式，本地可以展示，但是发布后无法显示
		2. html方式：如果用相对路径，本地显示裂图，但是发布后可以展示；如果使用绝对路径，本地可以展示，但是发布后无法展示... 
		3.  ![[assets/image.jpg]]
		4. <img src="\assets\image.jpg" style="zoom: 10%"/>
		5. ![test](https://www.notion.so/Life-Wiki-178a97ac39004465af1a32ad30d88375#7bdcd3cffa454ce8aaeef25959833d6b)
	
	 -- 可能的解决方式：1. 使用[[图床]]， 2. 使用插件：Obsidian-local-img-plugin
3. ⭕html代码块里面的页面链接，无法产生双链，在graph里无法展示