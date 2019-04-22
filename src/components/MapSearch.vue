<template>
  <div class="row">
    <div class="col-12 col-lg-6">
      <div id="map"></div>
      <input id="pac-input" class="controls m-2 px-2" type="text" placeholder="Enter Address...">
      <div>
        <span>Price:</span>
        <i id="price-1" v-on:click="price(1)" class="fas fa-dollar-sign pl-1"></i>
        <i id="price-2" v-on:click="price(2)" class="fas fa-dollar-sign pl-1"></i>
        <i id="price-3" v-on:click="price(3)" class="fas fa-dollar-sign pl-1"></i>
      </div>
      <div>
        <span>Has Produce:</span>
        <i class="fas fa-apple-alt pl-1"></i>
      </div>
    </div>
    <div class="col-12 col-lg-6">
      <div class="d-flex-col align-items-center">
        <h1>Closest Stores</h1>
        <div
          class="d-flex justify-content-between p-2 results"
          v-for="store in display_stores"
          :key="store.id"
        >
          <div>
            <span class="heavy-text pr-2">{{ store.tags.name }}</span>
            <span class="light-text">{{ store.dist.toString().slice(0, 3) }} mi</span>
          </div>
          <div class="d-flex">
            <div v-if="store.tags.shop in {'supermarket':0, 'organic':0}">
              <i class="fas fa-apple-alt"></i>
            </div>
            <div>
              <i v-for="i in store.tags.price" class="fas fa-dollar-sign pl-1"></i>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display_stores: [],
      all_stores: [
        {
          type: "node",
          id: 265837170,
          lat: 42.8995639,
          lon: -78.8787798,
          tags: {
            name: "Holly Farms",
            shop: "convenience",
            price: 2
          }
        },
        {
          type: "node",
          id: 414392643,
          lat: 42.9191243,
          lon: -78.8767071,
          tags: {
            name: "Lexington Co-op",
            shop: "organic",
            price: 3
          }
        },
        {
          type: "node",
          id: 566210891,
          lat: 42.9478503,
          lon: -78.8426688,
          tags: {
            name: "Dash's Market",
            shop: "supermarket",
            price: 2
          }
        },
        {
          type: "node",
          id: 629520975,
          lat: 42.9587374,
          lon: -78.8789928,
          tags: {
            name: "Save-a-Lot",
            shop: "supermarket",
            price: 1
          }
        },
        {
          type: "node",
          id: 714220178,
          lat: 42.8719731,
          lon: -78.8070933,
          tags: {
            name: "Clinton Street Mini-Mart",
            shop: "convenience",
            price: 2
          }
        },
        {
          type: "node",
          id: 768716991,
          lat: 42.8991878,
          lon: -78.8736134,
          tags: {
            name: "Allentown Trading Post",
            shop: "convenience",
            price: 2
          }
        },
        {
          type: "node",
          id: 768721742,
          lat: 42.8992851,
          lon: -78.8712879,
          tags: {
            name: "Bill's Food Mart",
            shop: "convenience",
            price: 2
          }
        },
        {
          type: "node",
          id: 927332730,
          lat: 42.9178485,
          lon: -78.8774729,
          tags: {
            name: "Globe Market",
            shop: "supermarket",
            price: 2
          }
        },
        {
          type: "node",
          id: 1386869696,
          lat: 42.858356,
          lon: -78.8303111,
          tags: {
            name: "Tops Markets",
            shop: "supermarket",
            price: 2
          }
        },
        {
          type: "node",
          id: 1892277134,
          lat: 42.948976,
          lon: -78.8288996,
          tags: {
            name: "Aldi",
            shop: "supermarket",
            price: 1
          }
        },
        {
          type: "node",
          id: 1978627974,
          lat: 42.9207792,
          lon: -78.8904671,
          tags: {
            name: "Guercio & Sons",
            shop: "supermarket",
            price: 2
          }
        },
        {
          type: "node",
          id: 3085720842,
          lat: 42.9600159,
          lon: -78.8172394,
          tags: {
            name: "TOPS",
            shop: "supermarket",
            price: 2
          }
        },
        {
          type: "node",
          id: 4196968701,
          lat: 42.90412,
          lon: -78.8164843,
          tags: {
            name: "Community Food & Meat Market",
            shop: "supermarket",
            price: 2
          }
        }
      ]
    };
  },
  methods: {
    dist(coords1, coords2) {
      return (
        ((Math.abs(coords1.lat) - Math.abs(coords2.lat)) ** 2)
        + ((Math.abs(coords1.lon) - Math.abs(coords2.lon)) ** 2)
        ** 0.5 ) / 2.1;
    },
    price(idx) {
      $("#price-1").css("color", "#ccc");
      $("#price-2").css("color", "#ccc");
      $("#price-3").css("color", "#ccc");
      if (idx > 2) {
        $("#price-3").css("color", "green");
      }
      if (idx > 1) {
        $("#price-2").css("color", "green");
      }
      if (idx > 0) {
        $("#price-1").css("color", "green");
      }
    },
    update_stores(coords) {
      // Find the closest stores
      var dists = [];
      for (var i in this.all_stores) {
        var store = this.all_stores[i];
        store.dist = this.dist(coords, store);
        dists.push(store);
      }
      dists.sort(function(a, b) {
        return a.dist - b.dist;
      });
      this.display_stores = dists.slice(0,3);

      console.log(this.display_stores);
      // Show the route to the closest store
    }
  },
  mounted() {
    var map = new google.maps.Map(document.getElementById("map"), {
      center: { lat: 42.8866, lng: -78.8793 },
      zoom: 13,
      mapTypeId: "roadmap"
    });

    // Add Markers

    for (var i in this.all_stores) {
      var marker = new google.maps.Marker({
        position: {
          lat: this.all_stores[i].lat,
          lng: this.all_stores[i].lon
        },
        map: map,
        title: this.all_stores[i].tags.name
      });
    }

    // Add GeoJSON Data
    map.data.loadGeoJson(
      "https://storage.googleapis.com/mapsdevsite/json/google.json"
    );

    // Create the search box
    var input = document.getElementById("pac-input");
    var searchBox = new google.maps.places.SearchBox(input);

    // Bias the SearchBox results towards current map's viewport.
    map.addListener("bounds_changed", function() {
      searchBox.setBounds(map.getBounds());
    });

    var markers = [];
    // Listen for the event fired when the user selects a prediction and retrieve
    // more details for that place.
    searchBox.addListener("places_changed", () => {
      var places = searchBox.getPlaces();

      if (places.length == 0) {
        return;
      }

      var coords = {
        lat: parseInt(places[0].geometry.location.lat(), 10),
        lon: parseInt(places[0].geometry.location.lng(), 10)
      };
      this.update_stores(coords);

      // Clear out the old markers.
      markers.forEach(function(marker) {
        marker.setMap(null);
      });
      markers = [];

      // For each place, get the icon, name and location.
      var bounds = new google.maps.LatLngBounds();
      places.forEach(function(place) {
        if (!place.geometry) {
          console.log("Returned place contains no geometry");
          return;
        }
        var icon = {
          url: place.icon,
          size: new google.maps.Size(71, 71),
          origin: new google.maps.Point(0, 0),
          anchor: new google.maps.Point(17, 34),
          scaledSize: new google.maps.Size(25, 25)
        };

        // Create a marker for each place.
        markers.push(
          new google.maps.Marker({
            map: map,
            icon: icon,
            title: place.name,
            position: place.geometry.location
          })
        );

        if (place.geometry.viewport) {
          // Only geocodes have viewport.
          bounds.union(place.geometry.viewport);
        } else {
          bounds.extend(place.geometry.location);
        }
      });
      map.fitBounds(bounds);
    });
  }
};
</script>

<style>
#map {
  height: 50vh;
}
.results {
  width: 100%;
  max-width: 500px;
}
#pac-input {
  background-color: #fff;
  font-family: Roboto;
  font-size: 15px;
  font-weight: 300;
  text-overflow: ellipsis;
  width: 80%;
}
#pac-input:focus {
  border-color: #4d90fe;
}
.heavy-text {
  font-weight: bold;
}
.light-text {
  color: #999;
  font-size: 80%;
}
.mw {
  max-width: 500px;
}
.w-150 {
  width: 150px;
}
.align-items-center {
  justify-content: center;
}
</style>
