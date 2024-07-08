<h1>3-minute deployment of the Phantom Beast Palu online service </h1>

<h2> Overview </h2>

<pre><code> Phantom Beast Palu is an open world survival production game developed by Pocketpair. The game will be released on January 18, 2024. In the game, players can collect magical creatures "Palu" in the vast world and send them to fight, build, do farm work, industrial production, etc. This article introduces how to quickly deploy the online service of Magic Beast Palu in the Alibaba Cloud Computing Nest console to realize online games with friends.
The estimated deployment time is 1~2 minutes. If you have any questions, please check the WeChat QR code at the bottom of the document and enter the group for communication ~
</code></pre>

<h2> Billing instructions </h2>

<p> the cost of phantom beast palu online service on the computing nest mainly involves: the selected vCPU and memory specifications, disk capacity, public network bandwidth
Billing methods include: annual package, monthly package, pay-as-you-go (hours)
The estimated cost can be seen in real time when the instance is created. </p>

<h2> Create an ECS </h2>

<h3> Step 1: Select Configuration </h3>

<ol>
<li> Service instance name (if there is no special requirement, keep the default);</li>
<li> Select the deployment region (you can select the city closest to you. If there are no special requirements, keep the default value);</li>
<li> choose the duration of payment (generally choose monthly, three months of discount is greater);</li>
<li><p> Select the configuration. Generally speaking, the higher the configuration, the smoother it will be. This game eats more memory, so the memory should be as much as possible above 16G (Pocketpair the official recommend configuration is 4-core 16G, see:<a href = "https://tech.palworldgame.com/dedicated-server-guide">Palworld tech guide</a>,CPU can choose 4-core, bandwidth recommend fixed bandwidth with unlimited traffic, low delay and better playing experience.
<img src="111.jpg" alt="111.jpg" />
Here ariyun has also recommend several configurations according to the number of players. everyone can do it as needed:</p>

<table>
<thead>
<tr>
<th> Package name </th>
<th> Description </th>
</tr>
</thead>
<tbody>
<tr>
<td> Support for 4-8 players </td>
<td>e-series 4-core 16G,3M bandwidth unlimited traffic </td>
</tr>
<tr>
<td> Support for 10-16 players </td>
<td>u1 series 4-core 32G,10M bandwidth unlimited traffic </td>
</tr>
<tr>
<td> Custom Package </td>
<td> ECS configuration can be freely selected, suitable for advanced DIY players </td>
</tr>
</tbody>
</table>

<p><img src="222.jpg" alt="222.jpg" /></p></li>
<li><p> Configure the server password (remember your password, use it later);</p></li>
<li> Configure the availability zone (if there are no special requirements, keep the default). </li>
<li> Configure the parameters of the online service in the advanced configuration column (use the default values without modification).
<img src="14.jpg" alt="14.jpg" />
After the configuration is completed, click Next to confirm the submission of the order. </li>
</ol>

<h3> Step 2: Create a service </h3>

<ol>
<li> on the service confirmation page, check agree to the terms of service, click "create now", followed by the payment process.
<img src="333.jpg" alt="333.jpg" /></li>
<li> when the prompt of successful submission appears, the service has been created. click "go to the list to view" to see that the service is being deployed.
<img src="444.jpg" alt="444.jpg" />
<img src="555.jpg" alt="555.jpg" /></li>
</ol>

<h3> Step 3: Enter the instance details </h3>

<ol>
<li> the service can be created in less than 1 minute. when the service status changes to "deployed", click the service instance ID to enter the service details. </li>
<li> by the time of this step, palu's server-side installation program has been preset in the image of the service, which is very convenient without manual replication.
<img src="666.jpg" alt="666.jpg" /></li>
<li> see "magic beast palu server address port", this is the IP address where you built the server, copy this address for the next operation.
<img src="777.jpg" alt="777.jpg" /></li>
</ol>

<h2> Login to the game </h2>

<p> Pre-conditions: You first need to buy Phantom Beast Palu (Palworld) on Steam. </p>

<ol>
<li><p> Log in to your Steam account. </p>

<p><img src="3.png" alt="3.jpg" /></p></li>
<li><p> Find the Phantom Beast in the Library and start the game.
<img src="4.png" alt="4.jpg" /></p></li>
<li><p> In the game menu, select "Join Multiplayer Game (Dedicated Server)"
<img src="5.png" alt="5.jpg" /></p></li>
<li><p> let players enter the address and port of your deployed computing nest service instance to play freely ~
<img src="6.png" alt="6.jpg" /></p></li>
</ol>

<p> so far, you have successfully built the magic beast palu Dedicated Server. please have fun with your friends here ~
|</p>

<h2> Palu Server Update </h2>

<h3> Automatic Updates </h3>

<p> enter operation and maintenance management-> update server version
<img src="upgrade.png" alt="upgrade.png" /></p>

<h3> Manual deployment </h3>

<p> Reference documentation
https://developer.aliyun.com/article/1428087</p>
