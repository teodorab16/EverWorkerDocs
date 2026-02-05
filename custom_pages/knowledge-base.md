---
title: Knowledge Base
fullscreen: false
hidden: false
---
<div id="kb-articles">
  <ul id="kb-list">
  </ul>
</div>

<script>
{`
// List your KB pages manually - easy to maintain
const kbPages = [
  { title: 'KB001: Troubleshooting Guide', slug: 'kb-001-troubleshooting' },
  { title: 'KB002: VPC Deployment', slug: 'kb-002-vpc-deployment' },
  // Add more as you create them
];

const list = kbPages.map(p => 
  '<li><a href="/docs/' + p.slug + '">' + p.title + '</a></li>'
).join('');
document.getElementById('kb-list').innerHTML = list;
`}
</script>
