
## gchart_line_chart.awk

Create [Google Charts](https://developers.google.com/chart/) from the command line. This script is one of the component taken from [ArcShell](https://arclogicsoftware.com/arcshell), a commercial automation framework for Bash.

A video going over the release of this script is [here](https://youtu.be/otCuhDZjfAY).

If you like my work follow me on [Twitter](https://twitter.com/poststop), [LinkedIn](https://bit.ly/ethan_ray_post), or [YouTube](https://www.youtube.com/channel/UCpra53Vkmw5xdyOiEpaf_Kw). You can also subscribe to my monthly newsletter [here](https://bit.ly/ethansnewsletter).  

----

The expected record format should look something like this.
 ```bash
 17_st,2019,1,3,19,57,15,0.00
 ```
Here is an explanation of each field.
```bash
metric_name,year,month,day,hour,minutes,seconds,metric_value
```
In the example below I parse the required fields from my data file. If you count the number of fields you might notice that I  have one extra column. This is an extra **metric_value**. The script actually supports up to 5 **metric_values**.
```bash
tail -100 "vmstats.csv" | awk -F"|" '{print $14","$3","$4","$5","$6","$7","$8","$16","$18}'
```
This is how we put it all together and pipe the data to the  awk script.
```bash
tail -100 "vmstats.csv" | \
   awk -F"|" '{print $14","$3","$4","$5","$6","$7","$8","$16","$18}' | \
   awk -v column_list="Time,Value,Average Value" -v log_scale=1 \
         -f gchart_line_chart.awk > vmstats.html
```
If you have any questions you can reach me by email at post.ethan@gmail.com.

Happy charting!


