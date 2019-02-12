I'm putting disaster recovery planning as a higher priority than monitoring. Your users will let you know 
when the application breaks - be it a minor inconvenience or a major catastrophe. Best to be prepared for
the worst. 

### You should know what your disaster scenario is.
1. Do you have a datacenter, or a primary availability zone? It's underwater.
2. 

### You should run your plan regularly. 

You should have your backed up data in more than one location.
   - You should have it close to production, in case of a small failure.
      - VM or machine failure.
      - Rack failure. 
   - You should have it far away from production, in case of a larger failure.
      - Datacenter underwater, vaporized
      - Raptor attack. 

If you have VMs, they should be backed up regularly.
If you have databases, they should be backed up constantly with periodic snapshots. 
   - pgsql: Streaming Replication (constant), pg_dump (snapshot)
   - Oracle: Redo/Archive Logs (constant), rman


You should validate your backed up data regularly.

If you have backed up VMs, restore them from backup. Spin it up, poke around.
If you have databases, restore them from back up. Run consistency checks. 
   - It's not a bad idea to restore a lower environment (like test) from a prod backup.
   - Some things need to be changed from prod to test - this is a great opportunity for scripting. 
