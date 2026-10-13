source("renv/activate.R")

# Invalidate the knitr cache when behdslabs changes. The cache (cache: true)
# only notices changes to a chunk's code, so after a package update chunks
# would keep showing results computed from the old data. cache.extra ties
# every chunk to the installed version and to a hash of the package data.
# knitr may already be loaded at this point (e.g. by renv), in which case
# its onLoad hook would never fire, so set the option directly.
local({
  set_cache_key <- function(...) {
    data_file <- system.file("data", "Rdata.rdb", package = "behdslabs")
    knitr::opts_chunk$set(cache.extra = paste(
      tryCatch(as.character(utils::packageVersion("behdslabs")),
               error = function(e) "none"),
      if (nzchar(data_file)) unname(tools::md5sum(data_file)) else "none"
    ))
  }
  if (isNamespaceLoaded("knitr")) set_cache_key()
  else setHook(packageEvent("knitr", "onLoad"), set_cache_key)
})

library(ggplot2)
behdslabs::ds_theme_set()
