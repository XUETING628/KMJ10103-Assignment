p_verbal <- bigclass %>% 
  ggplot(aes(x = Verbal)) + 
  geom_histogram(binwidth = 50, fill = '#D55E00', color = 'white', alpha = 0.8) + 
  labs(title = 'Distribution of Verbal Scores', x = 'Verbal Score', y = 'Frequency') + 
  theme_minimal() + 
  theme(plot.background = element_rect(fill = 'white'),
        panel.background = element_rect(fill = 'white'),
        axis.title.x = element_text(size = 18),
        axis.title.y = element_text(size = 18),
        axis.text.x = element_text(size = 14),
        axis.text.y = element_text(size = 14))
plotly_verbal <- ggplotly(p_verbal)
htmlwidgets::saveWidget(plotly_verbal, file = 'media/plots/verbal_scores_histogram.html', selfcontained = TRUE)
