# R code for Weight distribution boxplot by sex
library(ggplot2)
library(plotly)

weight_boxplot_sex_plot <- ggplot(bigclass, aes(x = sex, y = weight, fill = sex)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "Weight Distribution by Sex", x = "Sex", y = "Weight") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

weight_boxplot_sex_plotly <- ggplotly(weight_boxplot_sex_plot)
htmlwidgets::saveWidget(weight_boxplot_sex_plotly, file = "media/plots/weight_distribution_boxplot_by_sex.html", selfcontained = TRUE)
