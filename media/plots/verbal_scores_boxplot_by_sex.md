# R code for Verbal scores boxplot by sex
library(ggplot2)
library(plotly)

verbal_boxplot_sex_plot <- ggplot(bigclass, aes(x = sex, y = Verbal, fill = sex)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "Verbal Scores by Sex (Boxplot)", x = "Sex", y = "Verbal Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

verbal_boxplot_sex_plotly <- ggplotly(verbal_boxplot_sex_plot)
htmlwidgets::saveWidget(verbal_boxplot_sex_plotly, file = "media/plots/verbal_scores_boxplot_by_sex.html", selfcontained = TRUE)
