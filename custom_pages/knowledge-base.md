---
title: Knowledge Base
fullscreen: false
hidden: false
---
<script>
  {`
    fetch('https://dash.readme.com/api/v1/categories/kb-articles/page')
      .then(res => res.json())
      .then(pages => {
        const list = pages.map(p => 
          '<li><a href="/docs/' + p.slug + '">' + p.title + '</a></li>'
        ).join('');
        document.getElementById('kb-articles').innerHTML = '<ul>' + list + '</ul>';
      });
    `}
</script>

<div id="kb-articles">Loading KB articles...</div>
