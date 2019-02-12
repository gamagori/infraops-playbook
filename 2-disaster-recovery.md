I'm putting disaster recovery planning as a higher priority than monitoring. Your users will let you know 
when the application breaks - be it a minor inconvenience or a major catastrophe. Best to be prepared for
the worst. 

I guess I'm conflating disaster recovery and backups. Because, why would you have backups, other than to
recover from a disaster? I guess there are other reasons like having prod-parity lower environments, but
the disaster reason is a big one. 

Plan for machine and human failures. 

This one doesn't feel as clear as lay-of-the-land. Needs work. 

### You should back up your data. 
1. What is the data you are responsible for?
   - Are you responsible for virtual machines?
   - Are you responsible for database data? 
2. Where do you back up your data?
   - Do you store it close to production?
      - This is useful for quick restores after faulty deploys, etc
   - Do you store it far away from production?
      - For example, near a test environment. 
      - This is useful for ensuring production parity. 
   - Do you store it far, far away from production?
      - Offline copy, in a bank vault or something.
      - This is useful if you get hit with ransomware or a meteor. 
3. How often do you back up your data? 
   - What data do your users need in a recovery scenario? 
   - Do you have the latest deployment?
   - Do you have up-to-the-hour/minute/second transaction data?
      - Do you need it? 


### You should validate your backed up data. 
1. How do you restore your data to a live machine?
2. How do you check to see that all of your data is on the machine?
3. How do you check to see that all of your data is correct?
   - Can you point and application at your data and run it?
      - Can you launch the VM?
      - Can you start the database and pass consistency checks? 

### You should plan for the worst. 
1. What do you do when once machine fails?
2. What do you do when half the machines fail?
3. What do you do when all the machines fail?
4. What do you do when the network is vaporized?
5. What do you do when the datacenter is vaporized? 
6. What do you do when your sysadmin is hit by a bus?
   - Do you have the root password?
6. What do you do when your DBA is hit by a bus?
   - Do you have your database passwords? 

### You should run your plan regularly. 


If you have VMs, they should be backed up regularly.
If you have databases, they should be backed up constantly with periodic snapshots. 
   - pgsql: Streaming Replication (constant), pg_dump (snapshot)
   - Oracle: Redo/Archive Logs (constant), rman

If you have backed up VMs, restore them from backup. Spin it up, poke around.
If you have databases, restore them from back up. Run consistency checks. 
   - It's not a bad idea to restore a lower environment (like test) from a prod backup.
   - Some things need to be changed from prod to test - this is a great opportunity for scripting. 
