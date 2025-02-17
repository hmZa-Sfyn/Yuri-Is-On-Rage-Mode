
<h1 align="center">🚀 Dive into My Epic <code>Projects</code> 🚀</h1>

<h5 align="center">Introducing a Game-Changer: <code>C%</code> - The New Frontier in Programming! <br> Crafted by <code>C Sharpers</code>, Exclusively for <code>C Sharpers</code>!</h5>

```csharp
// this is not c# , this is c% (C Modulo)
class Hanoi {	
	void Solve(int n, char a, char b, char c) {
		if(n > 0) {
			Solve(n-1, a, c, b);
			System.Console.WriteLine("{0} -> {1}", a.ToString(), c.ToString());
			Solve(n-1, b, a, c);
		}
	}
	
	shared void Main() {
		new Hanoi().Solve(3, 'A', 'B', 'C');
	}
}
```

<h5 align="center">🔥 Level Up with the Revamped <code>Roobi</code> Language! 🔥 <br> A New Era for <code>Rubers</code>, Built by <code>Rubers</code>!</h5>

```ruby
# this is recognized as Roobi!
require "net/http"

c = Net::HTTP::Client.new

res = c.send do |req|
  req.url = "https://google.com"
  req.method = "GET"
end

puts res.body
```

<h5 align="center">💻 Enter the World of <code>Wax-Java</code> - Now with Extra Shine! 💻 <br> Tailored for <code>Lispers</code>, by <code>Lispers</code>!</h5>

```lisp
;; Poisson-Disk sampling
;; Based on paper:
;; https://www.cs.ubc.ca/~rbridson/docs/bridson-siggraph07-poissondisk.pdf
;; and Daniel Shiffman's p5.js implementation:
;; https://editor.p5js.org/codingtrain/sketches/4N78DFCXN

(@include math)

(@define K 30) ; "the limit of samples to choose before rejection in the algorithm"

;; distance square
(func dist2 (param x0 float) (param y0 float) (param x1 float) (param y1 float) (result float)
	(let dx float (- x0 x1))
	(let dy float (- y0 y1))
	(return (+ (* dx dx) (* dy dy)))
)

(func poissondisk
	(param W int) (param H int)         ; width, height
	(param r float)                     ; radius
	(param samples (arr (vec 2 float))) ; to be populated; can also be pre-filled with fixed points

	(local grid (arr int) (alloc (arr int)))
	(local active (arr (vec 2 float)) (alloc (arr (vec 2 float))))

	(let w float (/ r 1.4142135624))
	(let r2 float (* r r))
	(let cols int (/ W w))
	(let rows int (/ H w))
	
	(for i 0 (< i (* cols rows)) 1 (do
		(insert grid (# grid) -1)
	))
	(let pos (vec 2 float) (alloc (vec 2 float) 
		(/ W 2.0)
		(/ H 2.0)
	))
	(insert samples (# samples) pos)
	(for i 0 (< i (# samples)) 1 (do
		(let col int (/ (get samples i 0) w))
		(let row int (/ (get samples i 1) w))
		(set grid (+ col (* row cols)) i)
		(insert active (# active) (get samples i))
	))

	(while (# active) (do
		(let ridx int (* (call random) (# active)) )
		(set pos (get active ridx))
		(let found int 0)
		(for n 0 (< n @K) 1 (do
			(let sr float (+ r (* (call random) r)) )
			(let sa float (* 6.2831853072 (call random)))
			(let sx float (+ (get pos 0) (* sr (call cos sa))))
			(let sy float (+ (get pos 1) (* sr (call sin sa))))
			(let col int (/ sx w))
			(let row int (/ sy w))
			(if (&&
				(> col 0)
				(> row 0)
				(< col (- cols 1))
				(< row (- rows 1))
				(= (get grid (+ col (* row cols))) -1)
			)(then
				(let ok int 1)
				(for i -1 (<= i 1) 1 (do
					(for j -1 (<= j 1) 1 (do
						(let idx int (+ (* (+ row i) cols) col j))
						(let nbr int (get grid idx))
						(if (<> -1 nbr) (then
							(let d float (call dist2 sx sy (get samples nbr 0) (get samples nbr 1)) )
							(if (< d r2) (then
								(set ok 0)
							))
						))
					))
				))
				(if ok (then
					(set found 1)
					(set grid (+ (* row cols) col) (# samples))
					(let sample (vec 2 float) (alloc (vec 2 float) sx sy))
					(insert active (# active) sample)
					(insert samples (# samples) sample)
				))
			))
		))
		(if (! found) (then
			(remove active ridx 1)
		))
	))

)

;; draw sample points to svg image
(func plotsamples (param W int) (param H int) 
	(param samples (arr (vec 2 float)))
	(result str)
	(let s str (alloc str "<svg version=\"1.1\" xmlns=\"http://www.w3.org/2000/svg\" width=\""))
	(<< s (cast W str))
	(<< s "\" height=\"")
	(<< s (cast H str))
	(<< s "\">")

	(for i 0 (< i (# samples)) 1 (do
		(<< s "<circle cx=\"")
		(<< s (cast (get samples i 0) str))
		(<< s "\" cy=\"")
		(<< s (cast (get samples i 1) str))
		(<< s "\" r=\"1\" fill=\"hsl(")
		(<< s (cast (/ i 5) str))
		(<< s ",100%,30%)\"/>")
	))

	(<< s "</svg>")
	(return s)

)

;; test poisson disk
(func main (result int)
	(let W int 400)
	(let H int 400)
	(let r int 4)
	(local samples (arr (vec 2 float)) (alloc (arr (vec 2 float))) )
	(call poissondisk W H r samples)
	(local s str (call plotsamples W H samples))
	(print s)
	(for i 0 (< i (# samples)) 1 (do
		(free (get samples i))
	))
	(return 0)
)
```
