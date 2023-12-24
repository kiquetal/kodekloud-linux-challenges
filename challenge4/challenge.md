- Find the "hidden" files in "/home/bob/preserved" directory and copy them in "/opt/appdata/hidden/" directory (create the destination directory if doesn't exist).
  / find the hidden files inside a folder

        find /home/bob/preserved -type f -name ".*" -exec cp {} /opt/appdata/hidden/ \;
    
- Find the "non-hidden" files in "/home/bob/preserved" directory and copy them in "/opt/appdata/files/" directory (create the destination directory if doesn't exist).

        find /home/bob/preserved -type f -not -name ".*" -exec cp {} /opt/appdata/files/ \;

-Find and delete the files in "/opt/appdata" directory that contain a word ending with the letter "t" (case sensitive).

        find /opt/appdata -type f -name "*t" -exec rm {} \;

- Create a "tar.gz" archive of "/opt/appdata" directory and save the archive to this file: "/opt/appdata.tar.gz"

        tar -czvf /opt/appdata.tar.gz /opt/appdata

-Add the "sticky bit" special permission on "/opt/appdata" directory (keep the other permissions as it is).

        chmod +t /opt/appdata      

- Make "bob" the "user" and the "group" owner of "/opt/appdata.tar.gz" file.

        chown bob:bob /opt/appdata.tar.gz

- The "user/group" owner should have "read only" permissions on "/opt/appdata.tar.gz" file and "others" should not have any permissions

        chmod 440 /opt/appdata.tar.gz

- Create a "softlink" called "/home/bob/appdata.tar.gz" of "/opt/appdata.tar.gz" file.
    
        ln -s /opt/appdata.tar.gz /home/bob/appdata.tar.gz

- The script should filter the lines from "/opt/appdata.tar.gz" file which contain the word "processed", and save the filtered output in "/home/bob/filtered.txt" file. It must "overwrite" the existing contents of "/home/bob/filtered.txt" file

  script filter lines
    
        
- Change all the occurrences of the word "yes" to "no" in all files present under "/opt/appdata/" directory.

        sed -i 's/yes/no/g' /opt/appdata/*
