# Oloop-Readme

Oloop — Lecteur de Musique Hybride (Local & Streaming Audius)
Oloop est une application Android moderne conçue entièrement avec Jetpack Compose qui combine la lecture de fichiers audio locaux et le streaming décentralisé via la plateforme Audius. Elle arbore un design sombre premium avec des accents dorés et propose une expérience utilisateur soignée (vinyle rotatif, animations de jaquette).

Fonctionnalités principales
Bibliothèque Locale
Scan de l'appareil : Détection automatique des fichiers audio locaux (MP3, FLAC, M4A, etc.) via le MediaStore Android.
Lecteur Audio robuste : Basé sur Media3 / ExoPlayer fonctionnant en tâche de fond via un MediaSessionService.
Contrôles complets : Lecture/pause, piste suivante/précédente, recherche (seek), mode aléatoire et répétition.
Égaliseur : Accès à l'égaliseur audio système.
Streaming décentralisé (Audius)
Tendances dynamiques : Explorez les morceaux tendances de la semaine, globalement ou filtrés par genre (Electronic, Rock, Pop, Hip-Hop...).
Top Artistes de la semaine : Algorithme exclusif qui classe les artistes les plus actifs de la semaine selon leur présence dans les tendances et leur nombre d'abonnés.
Recherche globale : Recherche de morceaux ou d'artistes sur la plateforme Audius.
Favoris & Blocage : Marquez vos titres préférés pour un accès rapide ou bloquez des artistes indésirables (filtre permanent).
Widget Écran d'Accueil
Glance Widget : Widget interactif affichant le titre en cours de lecture, l'artiste, et des boutons de contrôle rapide (Play/Pause, Suivant, Précédent) synchronisés en temps réel avec le service de lecture.
Cache local & Optimisations
Caching intelligent : Mise en cache locale des données de l'API Audius (SharedPreferences + JSON) pour économiser la bande passante et accélérer l'affichage (invalidation automatique après expiration).
Gestion intelligente des jaquettes : Résolution optimale de jaquette préférée (480x480) et fallback automatique sur les serveurs miroirs d'Audius en cas d'indisponibilité.
Stack Technique
Composant	Technologie	Version
Langage	Kotlin	2.3.20
UI Framework	Jetpack Compose	BOM 2026.03.00
Playback Engine	Media3 ExoPlayer	1.10.0
Chargement d'images	Coil	2.7.0
Réseau	Retrofit + OkHttp	2.11.0 / 4.12.0
Widget	Jetpack Glance	1.1.1
Versionning Java	Java 17 / JVM Target 11	—
Min SDK	API 24 (Android 7.0)	—
Target SDK	API 36 (Android 16)	—
Architecture du Projet
Le projet suit une structure claire séparant l'UI, la gestion des données et le service de lecture en arrière-plan :

app/src/main/java/com/example/audiopure/
├── AudioPureApp.kt              # Configuration globale (Coil, Cache)
├── MainActivity.kt              # Point d'entrée de l'application (bypass de connexion)
├── PlaybackService.kt           # Service Media3 de lecture en arrière-plan
├── AudioWidget.kt               # Code du widget Glance pour l'écran d'accueil
│
├── data/
│   ├── api/
│   │   └── AudiusApi.kt         # Client Retrofit pour l'API Audius v1
│   ├── local/
│   │   ├── AudiusCacheManager.kt        # Système de cache API générique
│   │   ├── TopArtistsCacheManager.kt    # Cache spécifique aux Top Artistes
│   │   ├── BlockedArtistsManager.kt     # Persistance des artistes masqués
│   │   ├── AudiusFavoritesManager.kt    # Gestion locale des favoris Audius
│   │   └── FollowedArtistsManager.kt    # Suivi des artistes suivis
│   └── models/
│       ├── AudiusModels.kt      # Modèles de données de l'API Audius
│       └── Models.kt            # Modèles de données locaux (AudioFile, etc.)
│
└── ui/
    ├── screens/
    │   ├── AudioPlayerScreen.kt  # Écran principal (Lecteur local & Audius)
    │   ├── AudiusFullPage.kt     # Module de navigation et recherche Audius
    │   └── ArtistDetailScreen.kt # Fiche détaillée d'un artiste
    ├── components/
    │   ├── PlayerComponents.kt   # Composants UI du lecteur (jaquette vinyle, progression)
    │   ├── LibraryComponents.kt  # Composants de la bibliothèque locale
    │   └── AudiusComponents.kt   # Composants UI réutilisables d'Audius
    └── theme/
        ├── Color.kt              # Palette de couleurs dorée et sombre
        ├── Type.kt               # Typographie (Montserrat...)
        └── Theme.kt              # Définition du thème Material3
