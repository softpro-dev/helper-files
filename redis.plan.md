5টি Redis use case আছে এই project-এ:

# ১. Driver Location GEO Cache (সবচেয়ে দরকারি)

এখন dispatch-এ প্রতিবার DB query করে সব driver location আনে → haversine sort করে
Redis GEOADD + GEORADIUS দিলে: nearest drivers instantly, no DB hit
Bonus: 60s TTL → driver app বন্ধ হলে auto-remove from online list

# ২. Dispatch State Persistence
dispatchMap এখন server memory-তে — server restart হলে সব active dispatch শেষ, rider আটকে যায়
Redis-এ HSET dispatch:{id} → restart-proof

# ৩. Directions API Cache (সহজতম শুরু)

প্রতি 5s driver location update → Google Maps API call
10 driver × 5s = ১ মিনিটে 120 billable call
Redis SET directions:{hash} EX 60 → same route 60s cached, cost কমে

# ৪. Socket.io Multi-Instance

এখন single Node process — horizontal scale করলে rider-driver different instance-এ → communicate করতে পারবে না
@socket.io/redis-adapter → একটা লাইন change, সব instance room share করবে

# ৫. Auth Rate Limiting

OTP abuse রোধ, JWT logout blacklist
শুরু করার জন্য সুপারিশ: Item 3 (directions cache) — সবচেয়ে কম risk, সাথে সাথে Google Maps API cost কমবে। Implement করবো?



====================
Recommended order: 3 → 1 → 2 → 4 → 5

Start with 3 (directions cache) — zero risk, immediate cost cut. Then 1 for real performance gain. 2 and 4 needed before going multi-instance.


==========
# Redis Setup

## Local (Mac)
```bash
brew install redis
sudo chown -R $(whoami) ~/Library/LaunchAgents
brew services start redis
redis-cli ping   # → PONG
```
 

`.env`:
```
REDIS_URL=redis://localhost:6379
```

## Server — Docker (production)
`docker-compose.yml`-এ Redis service already add করা আছে।
`docker-compose up` দিলেই Redis container উঠবে — আলাদা কিছু লাগবে না।

`.env.prod`:
```
REDIS_URL=redis://redis:6379
```

## Server — Bare-metal (Docker ছাড়া)
```bash
sudo apt install redis-server -y
sudo systemctl enable redis-server
sudo systemctl start redis-server
redis-cli ping   # → PONG
```
`.env`:
```
REDIS_URL=redis://localhost:6379
```

## Verify (যেকোনো environment)
```bash
redis-cli monitor
# তারপর /places/directions API call করো → SET/GET command দেখবে
```

## Cache TTLs (implemented)
| Endpoint | TTL |
|---|---|
| `/places/directions` | 60s |
| `/places/autocomplete` | 300s |
| `/places/reverse-geocode` | 3600s |
| `/places/detail` | 86400s |

> Redis না থাকলে / REDIS_URL না দিলে → সব request Google Maps-এ fall through করে। Safe fallback.