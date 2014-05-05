!SLIDE

# the future <br/> is _primitive_

_<br/>map([softprops](http://github.com/softprops))&nbsp;_

_.flatMap(Oslo)&nbsp;_

!SLIDE
<h1 class="huge">our story,<h1>
<h1 class="huge">the sea.</h1>
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
enough! scrap this and start over with <em>_</em>.
</h1>

!SLIDE
<h1 class="huge">
<em>a <strong>healthy</strong> & <strong>sustainable</strong> way to live?</em>
</h1>

!SLIDE

<h1 class="huge">&ldquo;you go to <strong class="shadow">war</strong> with the <strong>algebra</strong> you&apos;ve got&rdquo;</h1>

&ndash;[@posco](https://twitter.com/posco) on [reality](https://twitter.com/softprops/status/439810801189531648)

!SLIDE

# _&ldquo;you go to war with the <strong>abstractions</strong> you were <strong>given</strong>&rdquo;_

<p class="mute">(armed with weapons you can not repair)</p>

!SLIDE

<h1 class="huge">&ldquo;the <strong>future</strong> is <strong>combinators</strong>&rdquo;</h1>

&ndash;[@posco](https://twitter.com/posco) on the design of [summingbird](https://github.com/twitter/summingbird)

!SLIDE

<h1 class="huge">the future is <em>_</em>.</h1>

!SLIDE
<h1 class="huge">less.<h1> 
<h1 class="huge">better.</h1>

!SLIDE


!SLIDE

# &ldquo;If you can't <strong>explain</strong> it <strong>simply</strong>, you don't <strong>understand</strong> it <strong>well</strong> enough&rdquo;

&mdash;[@einstein](http://en.wikipedia.org/wiki/Albert_Einstein)

!SLIDE

<h1 class="huge">import scala.<em>_</em></h1>
<p class="shadow">src of inspiration</p>

!SLIDE

<h1 class="huge center">case study: <em>&ldquo;Futures&rdquo;</em></h1>

!SLIDE

<h1 class="huge right">the <strong>right</strong><br/>kind of<br/><strong>complex</strong></h1>

!SLIDE

* _fixed in definition_
* _value-oriented_
* _simple to explain_
* _documented_
* _isolated_
* _honest_
* _resourceful_

!SLIDE
<div class="center">
<h1 class="huge"><img src="/main/sparkle.png"/>primitives<img src="/main/sparkle.png"/><h1>
</div>

!SLIDE

<h1 class="hugish"><em>Libraries</em> make <em>Promises</em>. <em class="pink">Applications</em> project on the <em class="pink">Future</em>.</h1>

!SLIDE

<h1 class="huge center"><span class="mute">enter</span> Future:<br/> a value, deferred.<h1>

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

<pre>
<span class="mute">import scala.concurrent
import concurrent.duration._
import concurrent.ExecutionContext.Implicits.global</span>
import odelay.Default.timer<br/>
val delay = odelay.Delay(3.seconds) {
  deliverPkg
}
</pre>

!SLIDE

# _delayed_ reactions

<pre>
<span class="mute">// on scheduled operation</span>
delay.future.onSuccess {
  case ship: Future[T] => pkgShipped
}
<span class="mute">// on success of scheduled future</span>
delay.future.flatMap(identity).onSuccess {
  case arrive: T => pkgArrived
}
</pre>

!SLIDE

# delayed cancellations

<pre>
delay.future.onFailure {
  case NonFatal(_) => abortShip
}
delay.cancel()
</pre>

!SLIDE

# periodic delays

<pre>
Delay.every(1.second)() {
  tick
}
</pre>

!SLIDE

<h1><strong>Timers</strong> are to <strong>Delays</strong> as <strong>ExecutionContexts</strong> are to <strong>Futures</strong>.</h1>

!SLIDE

# how to survive
# in the woods

<pre>
odelay.jdk.JdkTimer
odelay.netty.NettyTimer
odelay.twitter.TwitterTimer
</pre>

!SLIDE

<h1 class="huge">take your time</h1>