db.visitors.insertMany([
  { name: "Alice", country: "USA" },
  { name: "Bob", country: "Canada" },
  { name: "Charlie", country: "USA" },
  { name: "David", country: "Canada" },
  { name: "Eve", country: "UK" },
]);

// Map function
var mapFunction = function() {
  emit(this.country, 1);
};

// Reduce function
var reduceFunction = function(key, values) {
  return Array.sum(values);
};

var mapReduceOptions = {
  out: "visitor_country_count" // Output collection
};

db.visitors.mapReduce(mapFunction, reduceFunction, mapReduceOptions);


db.visitors.aggregate([
  {
    $group: {
      _id: "$country",
      count: { $sum: 1 },
    },
  },
]);



db.visitor_country_count.find();
