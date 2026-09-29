name: GitHub Metrics

on:
  schedule:
    - cron: "0 6 * * *"

  workflow_dispatch:

  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  github-metrics:
    runs-on: ubuntu-latest

    steps:
      - name: Generate GitHub Metrics
        uses: lowlighter/metrics@latest

        with:
          token: ${{ secrets.METRICS_TOKEN }}

          user: ${{ github.repository_owner }}

          filename: github-metrics.svg

          template: classic

          config_timezone: America/Sao_Paulo

          base: header, activity, community, repositories, metadata

          config_order: base.header, languages, isocalendar, activity, repositories, achievements

          # Linguagens mais utilizadas
          plugin_languages: yes
          plugin_languages_ignored: html, css
          plugin_languages_details: percentage
          plugin_languages_threshold: 2%
          plugin_languages_limit: 8
          plugin_languages_sections: most-used
          plugin_languages_indepth: yes

          # Calendário de commits
          plugin_isocalendar: yes
          plugin_isocalendar_duration: half-year

          # Atividade recente
          plugin_activity: yes
          plugin_activity_limit: 5
          plugin_activity_days: 30
          plugin_activity_filter: all

          # Repositórios
          plugin_repositories: yes
          plugin_repositories_featured: ""

          # Conquistas
          plugin_achievements: yes
          plugin_achievements_threshold: C
          plugin_achievements_secrets: yes
          plugin_achievements_display: compact
