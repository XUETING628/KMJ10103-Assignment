# R code for Height vs Weight scatterplot by sex
library(ggplot2)
library(plotly)

height_weight_scatterplot_sex_plot <- ggplot(bigclass, aes(x = height, y = weight, color = sex)) +
  geom_point(alpha = 0.7, size = 3) +
  scale_color_manual(values = c("M" = "#0072B2", "F" = "#CC79A7")) +
  labs(title = "Height vs. Weight by Sex", x = "Height", y = "Weight") +
  theme_minimal() +
  theme(plot.background = element_rect(fill = "white"),
        panel.background = element_rect(fill = "white"),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14))
  
height_weight_scatterplot_sex_plotly <- ggplotly(height_weight_scatterplot_sex_plot)
htmlwidgets::saveWidget(height_weight_scatterplot_sex_plotly, file = "media/plots/height_weight_scatterplot_by_sex.html", selfcontained = TRUE)
