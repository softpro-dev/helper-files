

# Create a new user in server root

# Create user with /var/www as home, no login shell
useradd -d /var/www -s /bin/bash -m webuser

# Set password
passwd webuser

# Add to www-data group (nginx/apache group)
usermod -aG www-data webuser










# Fix ownership of /var/www from root
chown -R webuser:www-data /var/www   # owner=webuser, group=www-data (nginx/apache)

# Folders: 755 — everyone can enter, only webuser can write
find /var/www -type d -exec chmod 755 {} \;

# Files: 644 — everyone can read, only webuser can write, no execute
find /var/www -type f -exec chmod 644 {} \;

# Writable dirs (uploads, cache, logs): 775 — www-data can write too
chmod -R 775 /var/www/your-app/storage
chmod -R 775 /var/www/your-app/public/uploads

# Quick reference: who can do what
# chmod 755 = rwxr-xr-x → owner: rwx | group: r-x | others: r-x
# chmod 644 = rw-r--r-- → owner: rw- | group: r-- | others: r--
# chmod 775 = rwxrwxr-x → owner: rwx | group: rwx | others: r-x
# chmod 700 = rwx------ → owner only, no one else

# Check current permissions
ls -la /var/www





# ─── DECISION GUIDE ────────────────────────────────────────────────────────────
#
# Q1: শুধু webuser deploy করবে, nginx শুধু read করবে?
#     → chown -R webuser:webuser /var/www
#     → chmod 755 folders, 644 files
#     → usermod -aG www-data  লাগবে না
#
# Q2: webuser deploy করবে + nginx-ও কিছু ফোল্ডারে লিখবে (cache/upload)?
#     → chown -R webuser:www-data /var/www
#     → chmod 755 folders, 644 files
#     → chmod 775 শুধু writable folders (storage, uploads, cache)
#     → usermod -aG www-data webuser  করো
#
# Q3: webuser একা সব করবে, বাইরে কেউ access পাবে না?
#     → chown -R webuser:webuser /var/www
#     → chmod 700 /var/www
#     ⚠ nginx ঢুকতে পারবে না — web app কাজ করবে না
#
# Q4: সব সহজ রাখতে চাই, security গুরুত্বপূর্ণ না?
#     → chmod 777  ← কখনো করো না, সার্ভার হ্যাক হওয়ার সহজ রাস্তা
#
# ✅ Production-safe default (বেশিরভাগ ক্ষেত্রে এটাই করো):
#     chown -R webuser:www-data /var/www
#     find /var/www -type d -exec chmod 755 {} \;
#     find /var/www -type f -exec chmod 644 {} \;
#     chmod -R 775 /var/www/your-app/storage
#     chmod -R 775 /var/www/your-app/public/uploads
#
# ───────────────────────────────────────────────────────────────────────────────
