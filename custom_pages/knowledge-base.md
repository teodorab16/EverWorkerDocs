---
title: Knowledge Base
fullscreen: false
hidden: false
---
<br />

<HTMLBlock>{`
<div id="kb-articles">Loading KB articles...</div>

<script>
const kbPages = [
  { title: 'KB001: How to collect VPC logs', slug: 'collect-vpc-logs' },
  { title: 'KB002: LLM API failing due to content management policy', slug: 'llm-api-fail-content-policy' },
];

const list = kbPages.map(p => 
  '<li><a href="/page/' + p.slug + '">' + p.title + '</a></li>'
).join('');

document.getElementById('kb-articles').innerHTML = '<ul>' + list + '</ul>';
</script>
`}</HTMLBlock>
