do this:
1) http://i.imgur.com/XdBrNER.png

// D_SEO_MODULE_JOURNAL_BLOG_FIX
if (substr($this->session->data['language'], 0, 2)) {
 	unset($parts[0]);
}
// D_SEO_MODULE_JOURNAL_BLOG_FIX - END

2) http://i.imgur.com/7AN6kMO.png

// D_SEO_MODULE_JOURNAL_BLOG_FIX
$url = '/' . substr($this->session->data['language'], 0, 2) . '/' . $this->model_journal3_blog->getBlogKeyword() . $url;
// D_SEO_MODULE_JOURNAL_BLOG_FIX - END
