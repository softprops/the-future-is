!SLIDE
# the future <br/> is _primitive_

_<br/>map([softprops](http://github.com/softprops))&nbsp;_

_.flatMap(Oslo)&nbsp;_

!SLIDE
<h1 class="huge">our story,<h1>
<h1 class="huge">the <span class="pink">sea</span></h1>
<h1><i class="fa fa-anchor"></i></h1>
<p class="pushdown"><em>it's (largely) our fault</em></p>

!SLIDE
<div class="top center">
  <h1 class="huge">
    noble intents
  </h1>
</div>
<div class="bottom center">
  <h1 class="huge">
   <em>sullied</em>
  </h1>
  <p>
  ( all you can eat )
  </p>
</div>

!SLIDE

# The water
# tastes &ldquo;great&rdquo;

(hindsight)

!SLIDE

<h1 class="huge">
%$#~! let's scrap this and start over with <em>_</em>.
</h1>

!SLIDE
<h1 class="huge">
<em>is this a <strong>healthy</strong> & <strong>sustainable</strong> way to live?</em>
</h1>

!SLIDE

<h1 class="huge">&ldquo;you go to <strong class="shadow">war</strong> with the <strong>algebra</strong> you&apos;ve got&rdquo;</h1>

&ndash; [@posco](https://twitter.com/posco) on ideals and [reality](https://twitter.com/softprops/status/439810801189531648) <i class="fa fa-twitter"></i>

!SLIDE

# _&ldquo;you go to war with the <strong>abstractions</strong> you were <strong>given</strong>&rdquo;_

<p class="mute">(armed with weapons you can not repair)</p>

!SLIDE

<h1 class="huge">&ldquo;the <strong>future</strong> is <strong>combinators</strong>&rdquo;</h1>
( not [plastics](https://www.youtube.com/watch?v=PSxihhBzCjk) )

&ndash;[@posco](https://twitter.com/posco) on the design of [summingbird](https://github.com/twitter/summingbird)

!SLIDE

<h1 class="huge">the future is <em>_</em>.</h1>

!SLIDE
<h1 class="gray">weniger,<h1>
<h1 class="gray">aber besser.</h1>
<h1 class="hugish">less,<h1>
<h1 class="hugish">better.</h1>
!SLIDE


!SLIDE

# &ldquo;If you can't <strong>explain</strong> it <strong>simply</strong>, you don't <strong>understand</strong> it <strong>well</strong> enough&rdquo; &mdash;[@einstein](http://en.wikipedia.org/wiki/Albert_Einstein)

!SLIDE

<h1 class="huge">import scala.<em>_</em></h1>
<p class="shadow">src of inspiration</p>

!SLIDE

<h1 class="huge center">case study: <em>&ldquo;Futures&rdquo;</em></h1>

!SLIDE

<h1 class="huge right">design for<br/>the <strong>right</strong><br/>kind of<br/><strong>complex</strong></h1>

!SLIDE

* _essence-ual_
* _value-oriented_
* _simple to explain_
* _isolate ( interface | execution )_
* _honest_
* _resourceful_

!SLIDE
<div class="center">
<h1 class="huge"><span class="pink"><i class="fa fa-magic"></i></span><img src="/main/sparkle.png"/><em>primitives</em><img src="/main/sparkle.png"/><h1>
</div>

!SLIDE

<h1 class="hugish"><em>Libraries</em> make <em>Promises</em>. <em class="pink">Applications</em> project on the <em class="pink">Future</em> promised.</h1>

!SLIDE

<h1 class="huge center">Future:<br/> a value,<br/>deferred.<h1>

!SLIDE

<pre class="huge">
onComplete(_)
</pre>

!SLIDE

<h1>A Future is an <em>interface</em>. <em>Execution</em> is a separate concern.</h1>
<pre>
<em>implicit executor: ExecutionContext</em>
</pre>


!SLIDE

<div class="top">
 <h1 class="center">&ldquo;Primitives&rdquo; as primitives.</h1>
</div>
<div class="bottom">
 <h1 class="center">Futures as &ldquo;primitives&rdquo;.</h1>
</div>

!SLIDE

<h1 class="huge center">case study: <em>&ldquo;Delays&rdquo;</em></h1>

!SLIDE

<h1><em>Delays</em> are to <em>operations</em> as <em class="pink">Futures</em> are to <em class="pink">values</em> for given <em>(Finite) Durations</em>.</h1>

!SLIDE

<h1 class="huge">#shipit</h1>

<pre>
<span class="mute">import scala.concurrent
import concurrent.duration._</span>
import odelay.Default.timer<br/>
val delay = odelay.Delay(3.seconds) {
  deliverPkg
}
</pre>

!SLIDE

# _delayed_ reactions_&trade;_

<pre>
<span class="mute">// on scheduled operation</span>
delay.<span class="blue">future</span>.onSuccess {
  case ship: Future[T] => pkgShipped
}
<span class="mute">// on success of scheduled future</span>
delay.<span class="blue">future</span>.flatMap(identity).onSuccess {
  case arrive: T => pkgArrived
}
</pre>

!SLIDE

# delayed cancellations

<pre>
delay.<span class="blue">future</span>.onFailure {
  case NonFatal(_) => abortShip
}
delay.<span class="pink">cancel</span>()
</pre>

!SLIDE

# periodic delays

<pre>
val delay = Delay.<span class="pink">every</span>(1.second)() {
  tick
}
// tick
// ...
// tick
// ...
// tick
// ...
delay.cancel()
</pre>

!SLIDE

<h1><strong>Timers</strong> are to <strong>Delays</strong> as <strong>ExecutionContexts</strong> are to <strong>Futures</strong>.</h1>

!SLIDE

<h1 class="huge">how to</h1>
<h1 class="huge">stay <span class="blue">alive</span></h1>
<h1 class="huge">in the woods</h1>
<p class="right shadow">make fire from sticks <em><i class="fa fa-fire"></i></em></p>

!SLIDE

<h1 class="blue center">pickup sticks</h1>
<pre class="center">
odelay.<span class="blue">jdk</span>.JdkTimer
odelay.<span class="blue">netty</span>.NettyTimer
odelay.<span class="blue">twitter</span>.TwitterTimer
com.<a href="https://github.com/softprops/odelay/issues/new?title=I%20found%20some%20sticks!" class="blue">you</a>.YourTimer
</pre>

!SLIDE
<pre>
implicit val <span class="pink">nodelay</span> = new Timer {
  <span class="blue">def apply(delay: FiniteDuration, op: => T)</span> =
    new PromisingDelay[T]
      with SelfCancellation[T] {
        completePromise(op)
    }
  <span class="blue">def apply(
    delay: FiniteDuration,
    init: FiniteDuration, op: => T)</span> =
    new PromisingDelay[T]
      with SelfCancellation[T] {
        op
        cancelPromise()
    }
}
</pre>

!SLIDE

<h1 class="center huge">take your time</h1>
<h1 class="center huge"><em><i class="fa fa-clock-o"></i></em></h1>

!SLIDE

<h1 class="center huge center pushdown">the future is <em>_</em>.</h1>
