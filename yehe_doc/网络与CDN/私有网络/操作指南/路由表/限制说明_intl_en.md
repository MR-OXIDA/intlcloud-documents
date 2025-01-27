- The default route table of a VPC cannot be deleted. 
- After a VPC is created, its route table will be automatically provided with a default route, indicating that all resources in this VPC are interconnected through the private network. This routing policy cannot be modified or deleted.
<table>
<tbody>
<tr>
<th>Destination</th>
<th>Next hop type</th>
<th>Next hop</th>
</tr>
<tr>
<td>Local</td>
<td>Local</td>
<td>Local</td>
</tr>
</tbody>
</table>

- Dynamic routing protocols such as BGP and OSPF are not supported.
- Routes can be published to CCN.The following routes can be published to CCN.
<table>
<tr>
<th>Next hop type</th>
<th>Publishing to CCN by default</th>
<th>Manually publishing or withdrawing</th>
<th>Description</th>
</tr>
<tr>
<td>Local</td>
<td>Supported</td>
<td>Not supported</td>
<td>Assigned by the system. The VPC IP range connecting to CCN will be automatically published to CCN, including primary and secondary CIDR blocks (except for TKE IP ranges).</td>
</tr>
<tr>

<td>CVM</td>
<td>Not supported</td>
<td>Supported</td>
<td>A custom route to CVM. When the IP range is all 0 or the routing policy is disabled, the route cannot be published to CCN.</td>
</tr>
<tr>
<td>HAVIP</td>
<td>Not supported</td>
<td>Supported</td>
<td>Custom route to HAVIP. When the IP range is all 0 or the routing policy is disabled, the routes cannot be published to CCN.</td>
</tr>
</table>

>?
> - A disabled custom route cannot be published to CCN.
> - A custom route should be withdrawn first before it can be disabled if it has been published to a CCN.

### Quota Limits
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>Number of route tables per VPC</td>
<td>10</td>
</tr>
<tr>
<td>Number of route tables associated with each subnet</td>
<td>1</td>
</tr>
<tr>
<td>Number of routing policies per route table</td>
<td>50</td>
</tr>
</table>
