---
tags:
  - Work
  - Codebase
---

```d2
network: {
  cellTower: {
    satellites: {
      shape: stored_data
      style.multiple: true
    }

    transmitter

    satellites -> transmitter: send
    satellites -> transmitter: send
    satellites -> transmitter: send
  }

  onlinePortal: {
    ui: {shape: hexagon}
  }

  data processor: {
    storage: {
      shape: cylinder
      style.multiple: true
    }
  }

  cell tower.transmitter -> data processor.storage: phone logs
}

user: {
  shape: person
  width: 130
}

user -> network.cellTower: make call
user -> network.onlinePortal.ui: access {
  style.stroke-dash: 3
}

api server -> network.onlinePortal.ui: display
api server -> logs: persist
logs: {shape: page; style.multiple: true}

network.data processor -> api server

```

