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
    { title: 'KB001: Troubleshooting Guide', slug: 'collect-vpc-logs' },
    { title: 'KB002: VPC Deployment', slug: 'llm-api-fail-content-policy' },
    // Add more as you create them
  ];

  const list = kbPages.map(p => 
    '<li><a href="/page/' + p.slug + '">' + p.title + '</a></li>'
  ).join('');
  document.getElementById('kb-list').innerHTML = list;
  `}
</script>
