# R code for Math scores histogram
library(ggplot2)
library(plotly)

# Generate Math scores histogram
math_hist_plot <- ggplot(bigclass, aes(x = Math)) +
  geom_histogram(binwidth = 50, fill = "#0072B2", color = "white") +
  labs(title = "Distribution of Math Scores", x = "Math Score", y = "Frequency") +
  theme_minimal() +
  theme(
    plot.background = element_rect(fill = "white"),
    panel.background = element_rect(fill = "white"),
    axis.title = element_text(size = 18),
    axis.text = element_text(size = 14)
  )

# Convert ggplot to plotly
math_plotly_plot <- ggplotly(math_hist_plot)

# Save the plot as an HTML widget
htmlwidgets::saveWidget(math_plotly_plot, file = "media/plots/math_scores_histogram.html", selfcontained = TRUE)
