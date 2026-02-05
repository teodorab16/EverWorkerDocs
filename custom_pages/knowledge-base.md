---
title: Knowledge Base
fullscreen: false
hidden: false
---
<div id="kb-articles">
  <ul id="kb-list" />
</div>

<script>
  {`
    // List your KB pages manually - easy to maintain
    const kbPages = [
      { title: 'KB001: How to collect VPC logs', slug: 'collect-vpc-logs' },
      { title: 'KB002: LLM API failing due to content management policy', slug: 'llm-api-fail-content-policy' },
    ];

    const list = kbPages.map(p => 
      '<li><a href="/page/' + p.slug + '">' + p.title + '</a></li>'
    ).join('');
    document.getElementById('kb-list').innerHTML = list;
    `}
</script>
