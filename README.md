# spark-with-r-basic-visualization-

hotttnesss <- track_metadata_tbl %>%
# Select artist_hotttnesss
select(artist_hotttnesss) %>%
# Binarize to is_hottt_or_nottt
ft_binarizer("artist_hotttnesss",
"is_hottt_or_nottt",
threshold = 0.5) %>%
# Collect the result
collect() %>%
# Convert is_hottt_or_nottt to logical
mutate(is_hottt_or_nottt = as.logical(is_hottt_or_nottt))
# Draw a barplot of is_hottt_or_nottt
ggplot(hotttnesss,
aes(is_hottt_or_nottt)) +
geom_bar()
