# scrape-snapshot
Scrapes snapshot to pin the IPFS files to your own node

# How it works

- `scrape.js` hits snapshots API to get all the proposals
- It writes the files proposals.txt and proposals.relayers.txt to use for `ipfs-sync`
- It then gets all the votes from the proposals from snapshots api
- It writes the files votes.txt and votes-relayers.txt
- It then runs `ipfs-sync` on these four files
- All the scripts are de-dupped so that this could run on a VM in the cloud, ping it once a day,
  and it will only append to the txt files. Then ipfs-sync already skips over dupes.

# TODO 

- Right now we are syncing with balancer's snapshot page rather than ours. Because ours is empty.
  We should fix this before going into production
- Get `ipfs-sync` to not boot out after batching the first 10 files to be synced over