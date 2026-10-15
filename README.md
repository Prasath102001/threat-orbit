# Threat Orbit: trace any IP to where it lives

A cinematic, single-file IP tracer. Type an IPv4/IPv6 address or a domain and:

1. **The address decodes** while three geolocation databases are queried in parallel.
2. **The globe swings to the target.** It's a dot-matrix (or satellite) Earth lit by the real Sun, so you can see at a glance whether it's day or night there.
3. **Real BGP routes arrive.** Up to 23 RIPE RIS route collectors on five continents fire arcs at the target's prefix, built from live looking-glass data.
4. **The network's physical footprint glows gold.** These are its data centres, from PeeringDB.
5. **Descend** dives into a 3D street-level view (map or satellite). It shows where each database placed the IP and how far they disagree.

There is no build step, no server and no API key. It's one `index.html`.

## What it tells you
| | Source |
|---|---|
| Location consensus (medoid of 3 databases, with outliers flagged) | ipwho.is, ipapi.co, ipquery.io |
| Day / night at the target, sun elevation, next sunrise or sunset | Computed in the browser |
| ASN, organisation, prefix, RPKI validity, BGP visibility, first seen in BGP | RIPEstat |
| Live AS paths from route collectors | RIPE RIS looking glass |
| RIR, net name, registration date, abuse contact | RDAP, RIPEstat |
| Reverse DNS | Google DNS-over-HTTPS |
| Open ports, CVEs, hostnames, tags | Shodan InternetDB |
| VPN / proxy / datacenter / Tor / risk score | ipquery.io, ipsnapshot, Tor Onionoo |
| Data-centre and exchange footprint | PeeringDB |

"Light floor" is the fastest possible round trip between you and the target: light in fibre over the great-circle distance. Real latency is always higher.

**On accuracy:** IP geolocation finds where a network is registered or homed, usually a city or a provider's hub, never a street address. Threat Orbit shows you where the databases disagree instead of hiding it.

## Controls
- `/` focuses the search; arrow keys move through suggestions.
- `S` switches between the dot-matrix and satellite globe.
- Drag to orbit the globe; scroll or pinch to zoom.
- `Esc` leaves the ground view.
- Share any trace as a link: `…/?ip=8.8.8.8`

## Privacy
Threat Orbit has no server of its own. Your browser talks directly to the services listed above, so they see your IP address and the address you look up, as with any website you visit. Recent searches and your Dots/Satellite choice are stored only in your own browser.

## Run it locally
Any static file server works, for example:

```bash
python -m http.server 8765
```

Then open http://localhost:8765.

## Credits
Globe imagery: NASA Blue Marble and Black Marble via three-globe. Country outlines: Natural Earth via world-atlas. Street maps: © OpenFreeMap / OpenMapTiles / OpenStreetMap contributors. Satellite imagery: © Esri, Maxar, Earthstar Geographics. Flags: FlagCDN. Fonts: Tektur, Chakra Petch and Kode Mono (Google Fonts). Built with three.js and MapLibre GL.

The free data services are meant for personal, non-commercial use; Shodan InternetDB in particular requires a licence for commercial use.
