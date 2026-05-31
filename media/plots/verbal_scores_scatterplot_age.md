# R code for Verbal scores scatterplot vs. age
library(ggplot2)
library(plotly)

verbal_scatterplot_age_plot <- ggplot(bigclass, aes(x = age, y = Verbal, color = sex)) +
  geom_point(alpha = 0.7, size = 3) +
  scale_color_manual(values = c("M" = "#009E73", "F" = "#CC79A7")) +
  labs(title = "Verbal Scores vs. Age", x = "Age", y = "Verbal Score") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))
  
verbal_scatterplot_age_plotly <- ggplotly(verbal_scatterplot_age_plot)
htmlwidgets::saveWidget(verbal_scatterplot_age_plotly, file = "media/plots/verbal_scores_scatterplot_age.html", selfcontained = TRUE)
