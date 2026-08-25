# Bellringers — moved

This app now lives inside Teacher Plate at **https://teacherplate.com/bellringers/**

Source is `~/.claude-apps/offload/bellringers/` (repo `kennady-scott/offload`).

What remains here is a path-preserving redirect. `index.html` and `404.html` are the same
stub, so any deep link — including `#/` routes — lands on the matching page at the new
address. It is JavaScript rather than a meta-refresh on purpose: a meta-refresh drops the
URL fragment, and every deep link into this app is a fragment.
