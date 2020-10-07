# apo design README

## WP Pusher說明
- 若須直接變動檔案請使用 WP Pusher，透過 Git Repository 修改，請勿在後台直接新增修改 CSS 樣式。
- 如需修改特定外掛、元件的樣式，請在後台替該元件上加入特定的 class 並更新 class 樣式放入此 repo 的 CSS檔。

<br/>

## 檔案結構說明-HTML
### 已進行變動的檔案（按名稱順序）
- `class\Module\Block\Block_5_View.php`（首頁下方文章列表 + 各處文章列表）
- `class\Module\Element\Element_Userlist_View.php`（作者列表）
- `class\Module\Hero\Hero_5_View.php` （首頁上方Hero Section）
- `class\Single\SinglePost.php`（文章內頁交換作者介紹及上下篇文章排序）
    - 有額外加一個`render_back_button`的 function，是最下面的回到列表按鈕
- `fragment\post\author-box.php`（單篇文章下方的作者框）
- `fragment\post\meta-post-1.php`（文章內頁上方作者、分類......資訊）
- `fragment\post\single-post-1.php`（文章內頁）
- `author.php`（特定作者文章列表頁）
- `functions.php`（WordPress子主題必須要有的檔案，目前內容僅有引入JNEWS子主題）

### 修改既有HTML結構步驟
1. 需要修改 JNEWS 原有 HTML 結構時，至 JNEWS 主題下搜尋相關`class`關鍵字，找到對應的 php 檔
2. 將該 php 檔按相同路徑複製到 JNEWS 子主題資料夾中
3. 修改子主題資料夾中的 php 檔
4. 將新增的修改檔案登錄到上方列表

### 如何調整blog post template內各區塊順序（[教學](https://support.jegtheme.com/forums/topic/change-blocks-order-in-post-template/)）

1. 到 `class\Single\SinglePost.php`。在`hooks`中找到

    `add_action( 'jnews_single_post_after_content', array( $this, 'next_prev_content_hook' ), 20 );
    add_action( 'jnews_single_post_after_content', array( $this, 'author_box_hook' ), 30 );
    ................................`
2. 調整其中的數字，越低越優先

<br/>

## 檔案結構說明-SASS
### 資料夾結構
- sass/components：通用元件（如字體、頁碼、編輯器內容等等）
- sass/helpers：
    - mixin：放`mixin`
    - variable：放顏色、字體變數
- sass/layout：通用區塊（如header、footer、sidebar、grid 等）
- sass/pages：各頁面設定
    - category
    - index
- sass/_reset.scss
- sass/style.scss：主檔案，從這邊引入其他元件，最上面的註解勿刪，是 WordPress 子主題必須的內容

### 命名規則
- 若需修改父 template 既有樣式，請直接覆蓋既有 class 即可（但需寫在對應元件/頁面檔中）
- 若需新增元件，請按下述規則命名
    - class prefix：custom-[position]-[content]
    - Grid System：沿用WPBakery自由排版套件、只新增客製 flex 部分

| media query                    | size   |
| ------------------------------ | ------ |
| default                        | xs     |
| @media (min-width:767px){}     | sm     |
| @media (min-width:992px){}     | md     |
| media (min-width:1200px){}     | lg     |
