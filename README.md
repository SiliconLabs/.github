## Troubleshooting

### My git clone stopped working with an LFS error. What could be the cause?

On December 13th, 2023, the Gecko SDK git LFS server changed and enabled a bandwidth quota based on your IP address.

- For existing clones, run the ```git reset –hard origin/<branch>``` command to update the LFS server. Alternatively, you can also use ```git config lfs.url = https://artifacts.silabs.net/artifactory/api/lfs/gsdk```. New clones will not have this issue since the LFS server will automatically be set correctly.
- Each unique IPs daily bandwidth usage will be tracked and capped at 30 GB per 24-hour period. When the quota is hit, the Git LFS server will throw a HTTP error with status 509 Bandwidth limit exceeded.

### How can I mitigate the risk of hitting the quota?

You will quickly hit this quota if you have automated processes that are repeatedly cloning the entire repository many times per day. Update your processes to cache the first clone of the repository and then have each iteration use a “git pull” instead of deleting and cloning from scratch.  Not only will this make your process much faster, it will effectively enable unlimited updates per day.  

### What if I have many machines behind a NAT firewall?

The quota is tracked by unique internet facing IP. If you are an organization that has many build machines that reach out to the internet with one IP, each machine will accumulate usage on the quota. To mitigate this, change your process so only one machine clones and pulls from the public git repository, and your internal machines read or copy the repository from that machine.  A very effective way to do this is by using the Git reference repository syntax on downstream machines ([https://git-scm.com/docs/git-clone](https://git-scm.com/docs/git-clone), navigate to section “—reference” ). Not only will this make your process much faster, it will effectively enable unlimited updates per day.   

### I have a fork of the GSDK repository

The LFS server of our repositories has changed, and any forks will need to sync with the parent to pickup the new .lfsconfig in the root directory of the repository. Forks can continue to use the main LFS server for pulls, but will be subject to the rate limit. If you need to modify LFS contents or want to remove the rate limit, you can clone the LFS repository to your own LFS server.

### Where do I go if I have questions?

The Silicon Labs technical support team will review and respond to any questions posted in the Community with a Tools tag here: [https://community.silabs.com/s/topic/0TO8Y000000eHD4WAM/tools?language=en_US](https://community.silabs.com/s/topic/0TO8Y000000eHD4WAM/tools?language=en_US).
