# R code for Age distribution histogram
library(ggplot2)
library(plotly)

# Generate Age distribution histogram
age_hist_plot <- ggplot(bigclass, aes(x = age)) +
  geom_histogram(binwidth = 1, fill = "#0072B2", color = "white") +
  labs(title = "Distribution of Age", x = "Age", y = "Frequency") +
  theme_minimal() +
  theme(
    plot.background = element_rect(fill = "white"),
    panel.background = element_rect(fill = "white"),
    axis.title = element_text(size = 18),
    axis.text = element_text(size = 14)
  )

# Convert ggplot to plotly
age_plotly_plot <- ggplotly(age_hist_plot)

# Save the plot as an HTML widget
htmlwidgets::saveWidget(age_plotly_plot, file = "media/plots/age_distribution_histogram.html", selfcontained = TRUE)
