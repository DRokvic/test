# Big Title
## Medium Title
### Small Title
Normal text

**bold text**

*cursive* 

example link [website](https://git.ista.ac.at/drokvic/flies_evodevo/-/blob/main/Preliminary.md?ref_type=heads)



```ruby
str(InsectSprays)

# InsectSprays is a simple count of insects found depending on a type of spray on cultivated land.
# For continuous data, best to actually show it.

# A quick and easy visualization is a bar graph ## always use the help function (eg stat_summary) to understand#
ggplot(InsectSprays, aes(x=spray, y=count)) +
  stat_summary(fun = mean, geom = "bar") +
  stat_summary(fun.data = mean_se, geom = "errorbar", width=.1, size=0.4) +
  scale_y_continuous(expand = c(0,0))

#But it's not actually very effective. Boxplot display the same information and more in a more effective way.
#Boxplot
##either:
ggplot(InsectSprays, aes(x=spray, y=count)) + geom_boxplot()

#or:
ggplot(InsectSprays, aes(x=spray, y=count)) +
  geom_boxplot(colour="red", outlier.shape=NA, fill=NA)

#We can also add more than one geom_ object, and add points on top of our boxplots

ggplot(InsectSprays, aes(x=spray, y=count)) +
  geom_jitter(width=0.15, alpha=.6) + 
  geom_boxplot(colour="red", outlier.shape=NA, fill=NA)

#Here we don't use geom_point, but a variant, geom_jitter, a convenient shortcut to geom_point(position = "jitter")
#There are A LOT of these "convenient short cuts" in ggplot, hence a lot of different ways to do a single thing.


#Instead of boxplots, we can chose the more minimalistic point ranges

ggplot(InsectSprays, aes(x=spray, y=count)) +
  geom_jitter(width=0.15, alpha=.6) + 
  stat_summary(fun.data = mean_cl_normal, colour="red")

#Crossbar (From package Hmisc) -> Another way to show spread of points.
ggplot(InsectSprays, aes(x=spray, y=count)) +
  geom_jitter(width=0.15, alpha=.6) + 
  stat_summary(fun.data = mean_cl_normal, geom="crossbar", colour="red", width=.4)

#We can also add an all type mean for reference :
ggplot(InsectSprays, aes(x=spray, y=count)) +
  geom_jitter(width=0.15, alpha=.6) + 
  stat_summary(fun.data = mean_cl_normal, geom="crossbar", colour="red", width=.4) +
  geom_hline(yintercept=mean(InsectSprays$count), linetype=2, alpha=0.5)

#Can make pretty. 
insect.plot <- ggplot(InsectSprays, aes(x=spray, y=count)) +
  stat_summary(fun.data= mean_cl_normal,geom="crossbar", aes(fill= spray), col=NA, size=0.4, width=.6, alpha=.4) +
  stat_summary(fun=mean, fun.min=mean, fun.max=mean, geom="crossbar", width=.6, size=.4) +
  theme(legend.position="none") +
  geom_jitter(aes(colour= spray), position=position_jitter(w=0.15,h=0), size=1.5) +
  geom_hline(yintercept=mean(InsectSprays$count), linetype=2, alpha=0.5)

insect.plot


# Saving graphs
setwd("C:/Users/drokvic/Documents/Dunja/Courses/Statistics")
#Either via clicking on "export", BUT: then, no influence on any parameters

# Suggested:
ggsave(insect.plot, file="Fig1.pdf", width=20, height=20, units="cm", useDingbats=F)


# I would generally advise saving graphs in PDF, this is much more practical and provides better quality.
# You can also modify your graph easily with a vector drawing software like Inkscape.

#You can also combine plots !
f1 <-plot_grid(orange.plot, air.plot, titanic.plot, insect.plot, ncol=2, labels=c("A","B","C","D"), axis =c("l", "l", "l", "l"), align="v")

#And then save
save_plot("Fig1.pdf", f1, base_height=20, base_width=20, units="cm")

save.image("recitation1_final.RData")
```
