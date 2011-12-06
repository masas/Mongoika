![][LogoImage]

Mongoika
========
Clojure MongoDB Library.

Usage
-----

    ;; Use mongoika namespace.
    (use 'mongoika)
    
    ;; Connect a MongoDB.
    (with-mongo [mongo {:host your-mongodb-host :port your-mongodb-port}]
      ;; Dynamic bind a database object.
      (with-db-binding (database mongo :your-db)
        ;; Insertion:
        (insert! :fruits {:name "Banana" :color :yellow :price 100})
        (insert! :fruits {:name "Apple" :color :red :price 80})
        
        ;; Multiple insertion:
        (insert-multi! :fruits
                       {:name "Lemon" :color :yellow :price 50}
                       {:name "Strawberry" :color :red :price 200})
        
        ;; Fetch all:
        (query :fruits) ; => [banana apple lemon strawberry]
        
        ;; Find:
        (restrict :color :red :fruits) ; => [apple strawberry]
        (restrict :price {> 100} :fruits) ; => [banana strawberry]
        
        ;; Sort:
        (order :price :asc :fruits) ; => [lemon apple banana strawberry]
        
        ;; Find and sort:
        (order :price :desc (restrict :color :yellow :fruits)) ; => [banana lemon]
        
        ;; Fetch first:
        (fetch-one (order :price :desc (restrict :color :yellow :fruits))))) ; => banana

License
-------

Copyright (C) 2011 Nyampass.

Distributed under the Eclipse Public License, the same as Clojure.

[LogoImage]: https://raw.github.com/yuushimizu/Mongoika/master/logo.png