# R code for Verbal scores average bar chart by sex
library(ggplot2)
library(dplyr)
library(plotly)

avg_verbal_by_sex <- bigclass %>% group_by(sex) %>% summarise(AvgVerbal = mean(Verbal))
verbal_barchart_avg_sex_plot <- ggplot(avg_verbal_by_sex, aes(x = sex, y = AvgVerbal, fill = sex)) +
  geom_bar(stat = "identity", alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "Average Verbal Scores by Sex", x = "Sex", y = "Average Verbal Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

verbal_barchart_avg_sex_plotly <- ggplotly(verbal_barchart_avg_sex_plot)
htmlwidgets::saveWidget(verbal_barchart_avg_sex_plotly, file = "media/plots/verbal_scores_barchart_avg_by_sex.html", selfcontained = TRUE)
