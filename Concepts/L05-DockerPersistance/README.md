---
sort: 6
---

# Docker Persistance

 * We have already seen the changes in a container are not persisted.
 * We could persist the change by commiting the container. But this would not be optimal for many situations
 * Consider a database server such as PostGreSQL, we would like it to have persisted data. However the we wouldn't want to have this as a part of the image.
 * There are 3 days to persist data in docker. Let's look at them below

{% include list.liquid all=true %}
