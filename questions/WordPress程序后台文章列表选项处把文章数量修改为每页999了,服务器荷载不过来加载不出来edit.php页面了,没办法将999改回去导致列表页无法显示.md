WordPress程序后台文章列表选项处把文章数量修改为每页999了,服务器荷载不过来加载不出来edit.php页面了,没办法将999改回去导致列表页无法显示

> 如标题所言

后台将设置为每页显示999文章导致辣鸡服务器直接加载不出来edit.php文件,如何操作???

### 解决方法1

去分类列表创建一个新分类,然后再分类列表下点击文章数量进去edit,然后就可以修改999了

### 解决方法2

修改php / mysql  这个我没找到如何该,好心的朋友可以留言,顺便附上chatgpt跟我讲的

---

了解您的问题。在WordPress中修改每页文章数量为999后，由于数量过大，导致edit.php页面无法加载。这种情况下，您可能需要通过编程的方式来解决这个问题。以下是一些可能的解决方案：

1. **使用`functions.php`文件**:
   在您的主题的`functions.php`文件中添加代码以修改每页的文章数量。虽然搜索结果中提到了可以通过`functions.php`文件修改每页的文章数量，但具体的代码片段没有显示出来【19†(source)】。
2. **利用WordPress钩子**:
   WordPress提供了一个钩子`edit_posts_per_page`，它允许您动态改变每页显示的文章数量。您可以在`functions.php`文件中添加如下代码：
   
   ```php
   function change_posts_per_page($posts_per_page, $post_type) {
       return 20;  // 或者您想要的任何其他数量
   }
   add_filter('edit_posts_per_page', 'change_posts_per_page', 10, 2);
   ```
   
   这段代码将每页的文章数量改为20【20†(source)】。
3. **检查`posts_per_page`参数**:
   如果您在使用自定义查询时遇到问题，确保您正确设置了`posts_per_page`参数。有时，某些查询参数可能会影响到`posts_per_page`的行为【21†(source)】。
4. **WordPress后台设置**:
   通常，您可以通过WordPress的后台设置来调整每页显示的文章数量。导航至`Settings` » `Reading`，然后修改`Blog pages show at most`选项的值。但由于您的edit.php页面无法加载，这个方法可能不适用于您的情况【22†(source)】。
5. **联系技术支持**:
   如果上述方法都无法解决您的问题，或者您不确定如何进行，可能需要联系WordPress的技术支持或者聘请专业的WordPress开发者来帮助您解决这个问题。

以上方法中的一些需要一定的技术知识，特别是涉及修改`functions.php`文件或使用WordPress钩子的方法。如果您不熟悉这些操作，强烈建议您联系专业人员以避免进一步的问题。
