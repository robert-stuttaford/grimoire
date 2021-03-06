### Example 0
[permalink](#example-0)

{% highlight clojure %}
{% raw %}
user=> (keep even? (range 1 10))
(false true false true false true false true false)
{% endraw %}
{% endhighlight %}


### Example 1
[permalink](#example-1)

{% highlight clojure %}
{% raw %}
;; comparisons among keep, map and for.

user> (keep #(if (odd? %) %) (range 10))
(1 3 5 7 9)
user> (map #(if (odd? %) %) (range 10))
(nil 1 nil 3 nil 5 nil 7 nil 9)
user> (for [ x (range 10) :when (odd? x)] x)
(1 3 5 7 9) 

user> (keep #(if(even? %) %) (range 10))
(0 2 4 6 8)
user> (map #(if (even? %) %) (range 10))
(0 nil 2 nil 4 nil 6 nil 8 nil)
user> (for [ x (range 10) :when (even? x)] x)
(0 2 4 6 8)

{% endraw %}
{% endhighlight %}


### Example 2
[permalink](#example-2)

{% highlight clojure %}
{% raw %}
;; Sieve of Eratosthenes by using 'keep'.

(defn keep-mcdr [f coll]
  (lazy-seq
     (when-let [x (first coll)]
       (cons x  (keep-mcdr f (f x (rest coll)))))))

(defn prime-number [n]
  (cons 1
	(keep-mcdr
	 (fn[x xs] (if (not-empty xs)
		     (keep #(if-not (zero? (rem % x)) %)
			   xs)))
	 (range 2 n))))

user> (prime-number 100)
(1 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97)
{% endraw %}
{% endhighlight %}


