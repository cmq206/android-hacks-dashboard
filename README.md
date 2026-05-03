# Live Android Hacks & Vulns Dashboard (2026)
**Auto-updates on load**: Fetches NVD/Android bulletins for new CVEs. Filter/search live. For Xiaomi/Redmi repairs.

<script>
// Live CVE fetch (runs in browser)
async function updateDashboard() {
  try {
    const res = await fetch('https://services.nvd.nist.gov/rest/json/cves/2.0?keywordSearch=android&resultsPerPage=10');
    const data = await res.json();
    const tableBody = document.getElementById('liveTable');
    tableBody.innerHTML = '';  // Clear
    data.vulnerabilities.slice(0,10).forEach(vuln => {
      const cve = vuln.cve.id;
      const desc = vuln.cve.descriptions[0].value.slice(0,100) + '...';
      const sev = vuln.cve.metrics?.cvssMetricV31?.[0]?.cvssData?.baseSeverity || 'N/A';
      tableBody.innerHTML += `<tr><td>${cve}</td><td>${sev}</td><td>${desc}</td></tr>`;
    });
  } catch(e) { console.log('Fetch fallback to static'); }
}
window.onload = updateDashboard;
</script>

## Live Table (Filters: Browser search)
<table id="liveTable">
<thead>
<tr><th>CVE</th><th>Severity</th><th>Description</th><th>Repro/Tools</th></tr>
</thead>
<tbody>
<!-- Static fallback + JS populates -->
<tr><td>CVE-2026-21385</td><td>High</td><td>Qualcomm graphics RCE</td><td>[mtkclient](https://github.com/bkerler/mtkclient)</td></tr>
<!-- Add your full rows from before -->
</tbody>
</table>

## Static Hacks (Actions-Updated)
| CVE | CPU | Patch_Status | Repro Steps |
|----|-----|--------------|-------------|
<!-- Paste full table here -->

**Sources**: NVD API [web:108], Bulletins [web:114]. Actions: See workflows.
