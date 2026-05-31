# R code for Verbal scores histogram
library(ggplot2)
library(plotly)

# Generate Verbal scores histogram
verbal_hist_plot <- ggplot(bigclass, aes(x = Verbal)) +
  geom_histogram(binwidth = 50, fill = "#D55E00", color = "white") +
  labs(title = "Distribution of Verbal Scores", x = "Verbal Score", y = "Frequency") +
  theme_minimal() +
  theme(
    plot.background = element_rect(fill = "white"),
    panel.background = element_rect(fill = "white"),
    axis.title = element_text(size = 18),
    axis.text = element_text(size = 14)
  )

# Convert ggplot to plotly
verbal_plotly_plot <- ggplotly(verbal_hist_plot)

# Save the plot as an HTML widget
htmlwidgets::saveWidget(verbal_plotly_plot, file = "media/plots/verbal_scores_histogram.html", selfcontained = TRUE)
