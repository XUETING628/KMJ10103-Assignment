# R code for Math scores boxplot by sex
library(ggplot2)
library(plotly)

math_boxplot_sex_plot <- ggplot(bigclass, aes(x = sex, y = Math, fill = sex)) +
  geom_boxplot(alpha = 0.7) +
  scale_fill_manual(values = c("M" = "#0072B2", "F" = "#D55E00")) +
  labs(title = "Math Scores by Sex (Boxplot)", x = "Sex", y = "Math Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "none")

math_boxplot_sex_plotly <- ggplotly(math_boxplot_sex_plot)
htmlwidgets::saveWidget(math_boxplot_sex_plotly, file = "media/plots/math_scores_boxplot_by_sex.html", selfcontained = TRUE)
