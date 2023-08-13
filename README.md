# CLSTR
Group triggers into 'clusters' and send &amp; receive messages between multiple clusters

# Example
```ts
extract obj_props

$.add(obj {
  OBJ_ID: 1,
  X: 15,
  Y: 15,
  GROUPS: 1g
})

@cluster::add('cluster_2', (curr_cluster) {
  curr_cluster.on('click', (_) { // we are not using the 'args' parameter (@array)
    1g.move(0, 10)
  })
})

@cluster::add('main_cluster', (_) { // we won't need to use the current cluster
    on(touch(), !{
        @cluster::find('cluster_2').message('click') // you can use an array as a second argument in order to pass arguments to the cluster
        // or use '@cluster::global().message('click')' to broadcast the message to all clusters
    })
})
```
