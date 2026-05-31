p_math <- bigclass %>% 
  ggplot(aes(x = Math)) + 
  geom_histogram(binwidth = 50, fill = '#0072B2', color = 'white', alpha = 0.8) + 
  labs(title = 'Distribution of Math Scores', x = 'Math Score', y = 'Frequency') + 
  theme_minimal() + 
  theme(plot.background = element_rect(fill = 'white'),
        panel.background = element_rect(fill = 'white'),
        axis.title.x = element_text(size = 18),
        axis.title.y = element_text(size = 18),
        axis.text.x = element_text(size = 14),
        axis.text.y = element_text(size = 14))
plotly_math <- ggplotly(p_math)
htmlwidgets::saveWidget(plotly_math, file = 'media/plots/math_scores_histogram.html', selfcontained = TRUE)
