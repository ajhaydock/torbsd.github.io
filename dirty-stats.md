Title: The Tor BSD Diversity Project: Quick-and-Dirty Static Reports
CSS: torbsd.css
Author: gman
Editors: attila
Data: 2015-10-30
X-Note: These lines at the top are multimarkdown metadata; leave them.


{{header.md}}

## Quick-and-Dirty Static Reports ##

This small project aims at producing simple, relevant reports about public Tor network relays for making broad conclusions related to network diversity. While primarily about providing a glance of the current state of the Tor network, some may find it useful for presentations or other times static, broad snapshots of Tor is necessary.

__TDP__ focuses primarily on operating system diversity, specifically as related to BSD Unix, but such diversity should account for percentages versus absolute numbers, average bandwidth per relay by operating system, plus variables such as geographical diversity.

Currently, the reports are generated by shell scripts after retrieving the data from [https://torstatus.rueckgr.at](https://torstatus.rueckgr.at). The shell scripts will be posted on our [GitHub repository](https://github.com/torbsd) as soon as they are in an intelligible form. However, the whole operation is being migrated to Sqlite as it's outgrown the initial aims.

### Current Reports ###

__[Bandwidth Rank by Country Code](bw-rank-cc.txt)__

Ranking in Kbps of bandwidth provided by each country code, along with the percentage of bandwidth provided by each country code.

__[Bandwidth Rank by Operating System](bw-rank-os.txt)__

Ranking in Kbps of bandwidth provided by each operating system, with the relevant percentages.

__[Operating Systems Count](os-count.txt)__

Count of relays by operating system or platform, along with the percentage of each on the Tor network.

__[Number of Relays per Country Code](relays-by-cc.txt)__

Number of relays by country code.

__[Country Codes without Public Tor Relays](tor-less-ccs.txt)__

This was was the first report created, based on the dearth of relays in a number of countries such as Pakistan, and the low number of relays in Brazil, India and Mexico.

{{footer.md}}