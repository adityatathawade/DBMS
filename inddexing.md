// Simple Index
db.visitors.createIndex( {
    name: 1
} ) ; 

// Compound Index
db.visitors.createIndex( {
    name: 1 , 
    age: 1 , 
    city: 1
} ) ; 

// Unique Index
db.visitors.createIndex( {
    name: 1 , 
    city: 1 ,
} , { unique: true } );

db.createCollection( "visitors" ) ;
db.visitors.insertMany( [  
    {
        "name": "Shubham" , 
        "department": "COMP" , 
        "age": 19 , 
        "year": "TE" , 
        "city": "Pune" , 
        "insem_marks": 130 ,
        "endsem_marks": 280 ,
    } , 
    {
        "name": "Kaustubh" , 
        "department": "IT" , 
        "age": 23 , 
        "year": "TE" , 
        "city": "Jalgaon" , 
        "insem_marks": 135 ,
        "endsem_marks": 310 ,
    } , 
    {
        "name": "Ram" , 
        "department": "ENTC" , 
        "age": 18 , 
        "year": "TE" , 
        "city": "Pune" , 
        "insem_marks": 125 ,
        "endsem_marks": 340
    } , 
    {
        "name": "Swaraj" , 
        "department": "COMP" , 
        "age": 22 , 
        "year": "SE" , 
        "city": "Pune" , 
        "insem_marks": 145 ,
        "endsem_marks": 320
    } , 
    {
        "name": "Manthan" , 
        "department": "IT" , 
        "age": 21 , 
        "year": "BE" , 
        "city": "Pune" , 
        "insem_marks": 150 ,
        "endsem_marks": 150
    } , 
    {
        "name": "Ayush" , 
        "department": "COMP" , 
        "age": 20 , 
        "year": "BE" , 
        "city": "Chandrapur" , 
        "insem_marks": 110 ,
        "endsem_marks": 180 
    } , 
]);


// Compute average INSEM and ENDSEM marks of all visitors
db.visitors.aggregate( [
    {
        $group: {
            _id: null,
            avg_insem_marks: { $avg: "$insem_marks" } , 
            avg_endsem_marks: { $avg: "$endsem_marks" }
        }
    } 
] ) ; 

// Compute count of visitors in each department
db.visitors.aggregate( [
    {
        $group: {
            _id: "$department" , 
            num_visitors: { $count: {} }
        }
    }
] ) ; 

// Compute average INSEM and ENDSEM marks by department
db.visitors.aggregate( [
    {
        $group: {
            _id: "$department" , 
            avg_insem_marks: { $avg: "$insem_marks" } , 
            avg_endsem_marks: { $avg: "$endsem_marks" }
        }
    }
] ) ; 

// Compute sum of INSEM and ENDSEM marks for each student
// belonging to COMP branch and determine the topper
db.visitors.aggregate( [
    {
        $match: {
            "department": "COMP"
        }
    } , 
    {
        $group: {
            _id: {
                name: "$name" , 
                age: "$age" , 
                city: "$city" , 
                department: "$department"
            } , 
            total_marks: { 
                $sum: { 
                    $add: [ "$insem_marks" , "$endsem_marks" ]
                }
            }
        }
    } , 
    {
        $sort: {
            total_marks: -1
        }
    } , 
    {
        $project: {
            "name": 1 , 
            "age": 1 , 
            "city": 1
        }
    } , 
    {
        $limit: 1
    }
]) ;
