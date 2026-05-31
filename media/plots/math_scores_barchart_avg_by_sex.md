# R code for Math scores average bar chart by sex
library(ggplot2)
library(dplyr)
library(plotly)

avg_math_by_sex <- bigclass %>% group_by(sex) %>% summarise(AvgMath = mean(Math))
math_barchart_avg_sex_plot <- ggplot(avg_math_by_sex, aes(x = sex, y = AvgMath, fill = sex)) +
  geom_bar(stat = "identity", alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#0072B2", "F" = "#D55E00")) +
  labs(title = "Average Math Scores by Sex", x = "Sex", y = "Average Math Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

math_barchart_avg_sex_plotly <- ggplotly(math_barchart_avg_sex_plot)
htmlwidgets::saveWidget(math_barchart_avg_sex_plotly, file = "media/plots/math_scores_barchart_avg_by_sex.html", selfcontained = TRUE)
