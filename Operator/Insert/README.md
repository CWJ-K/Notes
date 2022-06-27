<!-- omit in toc -->
# Introduction
Take note of insert 

<br />

<!-- omit in toc -->
# Table of Contents



# MySQL: INSERT ON DUPLICATE KEY UPDATE
* update the existing row with the new values instead

    INSERT INTO table (column_list)
    VALUES (value_list)
    ON DUPLICATE KEY UPDATE
    c1 = v1, 
    c2 = v2,
    ...;
