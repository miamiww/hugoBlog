+++
title = "Shodan Stories Day 66: Making Cement in Tuban"
date = 2019-03-10T16:17:35-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a search just for everything that's a customer of [PT Telkom Indonesia](https://en.wikipedia.org/wiki/Telkom_Indonesia), an Indonesian ISP.

## Tuban Cement Factory on 180.250.182.241
I ended up picking the first result because I saw on Shodan, in the town of [Tuban on Java](https://en.wikipedia.org/wiki/Tuban), that it was running this warning on the telnet port, 23.

```
*****************************************************************************

                           PT Holcim Indonesia Tbk
                          Astinet Router to STO Kerek
                                 Tuban Plant

   WARNING:     This is a private system. Unauthorized access to or
                use of this system is strictly prohibited. By continuing,
                you acknowledge your awareness of and concurrence with the
                acceptable use policy of PT Holcim Indonesia Tbk.
                Unauthorized users may be subject to criminal prosecution
                under the law and are subject to disciplinary action under
                PT Holcim Indonesia Tbk policies.


*****************************************************************************

User Access Verification

Username:
```
This warned me off trying to probe it too much, so I'm just going off what I see on Shodan. It's also running a [Cisco IOS](https://en.wikipedia.org/wiki/Cisco_IOS) HTTP login on port 80. Cisco IOS is Cisco's router software, so I feel safe in assume that this is a router. It also says "Astinet Router" in the warning, and after looking into it I've found that [Astinet](https://indihomesukabumi.com/astinet/) is the name of PT Telkon's internet service. They have a nice little ad.
{{< youtube pxX3a1ZBPIs >}}
STO Kerek, I think is the name of a [fiber network in the Tuban area](https://trustklik.wordpress.com/sto-kerek/).

So where is the router? We actually have a ton of clues from the warning. It belongs to [PT Holcim Indonesia Tbk](https://www.holcim.co.id/en), the Indonesian branch of a [global cement and building materials company](https://www.lafargeholcim.com/). It did not take me very much Googling to find that [Holcim runs](http://www.globalcement.com/news/item/3922-holcim-set-to-operate-new-us-350m-tuban-ii-cement-plant) [a cement factory in Tuban](https://www.lafargeholcim.com/lafargeholcim-completes-tuban-plant-project-indonesia), which they call the [Holcim Tuban Plant](https://www.holcim.co.id/en/lokasi/tuban-plant/3001), hence the name on the router, Tuban Plant.

Here it is on Google maps.
![](/images/100Days/Day66/plant.png)
![](/images/100Days/Day66/plant2.png)
![](/images/100Days/Day66/plant3.png)

Feels so strange to reach out like this and find yourself at a cement factory in Indonesia. It must be so humid there. Imagine watching the sunset from the top of one of those towers, your shift finishing. Maybe you're making some repairs, and you're ready to get home but you know you've got an hour bike ride ahead of you.

Where does the cement go? What buildings have been made from it? Holcim's press releases mentioned its proximity to the coast and to shipping lines as a reason they built the factory there. So it could be anywhere. Maybe there's some in new construction here in New York. See you tomorrow.
