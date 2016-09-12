# Working Draft: KVAL (Key Value Access Language) 

*Grammar* for accessing K,V databases with a bit more ease. First binding intended to be for Golang's BoltDB. 

##Operations:

###Basic inserts and gets

      INS Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key :: Value
      INS Prime Bucket >> Secondary Bucket >> Tertiary Bucket
      GET Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key :: Value
      GET Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key
      GET Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> {PAT}
      GET Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> _ :: Value
      GET Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> _ :: {PAT}
      LIS Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key
      LIS Prime Bucket >> Secondary Bucket >> Tertiary Bucket 
      DEL Prime Bucket >> Secondary Bucket >> Tertiary Bucket
      DEL Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key
      DEL Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key :: _
      REN Prime Bucket >> Secondary Bucket >> Tertiary Bucket >>>> Key => Key
      REN Prime Bucket >> Secondary Bucket >> Tertiary Bucket => Third Bucket

###Functions

      INS   Insert
      GET   Get values
      LIS   Check existence
      DEL   Delete
      REN   Rename

###Operators

      >>    Bucket:Bucket relationship
      >>>>  Bucket:Key relationship
      ::    Key::Value releationship
      =>    Name assignment
      _     Nil

###Capabilities

      {PAT} Given a regex {PAT} for Key XOR Value, find match.

###Restrictions

      Must be >= 1 Buckets for data. 

###Examples

      Bucket B exists inside Bucket A:                A >> B  
      Check existence of Bucket B inside Bucket A:    LIS A >> B              [Return: True]
      Get key value pairs in B:                       GET A >> B
                                        
      Key K1 exists inside Bucket A:                  A >>>> K1
      Check K1 exists inside Bucket A:                LIS A >>>> K1
      Get value for K1:                               GET A >>>> K1
      Add value for K1:                               INS A >>>> K1 :: V1
      Delete K1 value:                                DEL A >>>> K1 :: _
      
      Delete A:                                       DEL A
      Delete B:                                       DEL A >> B
      
      Rename K1:                                      REN A >>>> K1 => K2
      Rename B:                                       REN A >>>> B => C
      
