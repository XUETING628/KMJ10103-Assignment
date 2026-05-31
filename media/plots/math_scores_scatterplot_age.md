# R code for Math scores scatterplot vs. age
library(ggplot2)
library(plotly)

math_scatterplot_age_plot <- ggplot(bigclass, aes(x = age, y = Math, color = sex)) +
  geom_point(alpha = 0.7, size = 3) +
  scale_color_manual(values = c("M" = "#0072B2", "F" = "#D55E00")) +
  labs(title = "Math Scores vs. Age", x = "Age", y = "Math Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))
  
math_scatterplot_age_plotly <- ggplotly(math_scatterplot_age_plot)
htmlwidgets::saveWidget(math_scatterplot_age_plotly, file = "media/plots/math_scores_scatterplot_age.html", selfcontained = TRUE)
