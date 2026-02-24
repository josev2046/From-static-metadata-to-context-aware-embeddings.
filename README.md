## From static metadata to context-aware embeddings.

<img width="993" height="559" alt="image" src="https://github.com/user-attachments/assets/b91f5768-dd39-4992-8bab-f198b32f9f35" />


Can't tire of hammering this to my students: the integration of multimodal AI into our data pipelines represents a fundamental shift in how we handle media today, and is here to stay. We are moving away from static files towards semantic data, where assets maintain an active, searchable awareness of their own content.

And of course, we had been here before. Back in 2018, I presented a paper at the FIAT/IFTA World Conference in Venice detailing my work with the BBC Archive and "The Blue Room" innovation hub. Our objective was to unlock a vast, historical video archive using the late IBM Watson Video Enrichment. By applying early Natural Language Understanding (NLU), we moved beyond manual metadata tagging, allowing journalists and researchers to query the archive in plain English. At the time, it was a significant step forward. However, looking back, that classic AI pipeline represents the legacy approach.

Back then, we relied on "stitched analysis". We ran separate, isolated models for audio, OCR, and computer vision, and then stitched the results together. The output was essentially a "bag of tags" - for example, [Sky: 90%], [Man: 80%], [Loud Noise]. The critical weakness of this approach was a complete lack of context. The system struggled to differentiate between a cooking show and a horror movie or newsflash on f* Brexit because it did not inherently understand how the visual, audio, and temporal components related to one another.

Today, we have undergone a change of paradigm. We have shifted to joint multimodal embeddings. Instead of isolated models, their engines ingest video, audio, and time simultaneously into a single vector representation. Nice. The output is inherently context-aware and time-sensitive. It understands relationships and actions as they unfold - recognising a "man chopping onions quickly" rather than just spotting a man and an onion.

This contextual awareness is exactly what allows for the robust governance paradigm we need today. In the context of global media archives and automated licensing, manual compliance review has become an immense bottleneck. When a broadcaster wants to syndicate historical footage, they require an ironclad level of assurance about what is actually in those tapes that basic metadata cannot provide.

To process this at scale, we need the right data infrastructure (think Pixeltable as the orchestrator) and use a declarative database model where AI models are treated as simple table columns. Instead of writing complex loops to process files, you declare a relationship. Through computed columns, the database automatically triggers the necessary API calls when a new video is ingested. It moves the logic directly to the data, employing incremental computing to only process new entries and automatically parse the unstructured JSON returns into structured, readable rows.

Lacking anything better to do with my time, I cobbled together an automated governance pipeline to give the students a real world use case - an "acid test" for historical archive ingest, so to speak - using this exact architecture to process a batch of unedited, decades-old news rushes. The objective being to automatically catalogue the footage while flagging broadcast-restricted elements like off-air journalist swearing, sudden crowd violence, and embargoed on-screen text. I used Twelve Labs and Pixeltable.

Because the system genuinely understands multimodal context, it can provide clear, contrasted explainability, such as approving standard broadcast packages without throwing false positives at intense, but non-violent, political debates, triggering a review flag by pinpointing the exact timecode a previously peaceful protest escalated into a physical clash with police, blocking restricted rushes from the syndication pool by reading handwritten "DO NOT BROADCAST" clapperboards via OCR or catching off-air reporters cursing about the weather under their breath in the audio track, while the camera was just pointing at a brick wall... - we are removing the guesswork from media moderation, every decision backed by temporal evidence extracted directly from the asset (caveat as we should, that hey, this is not a deterministic solution, we are just more or less confident of results, and must watch out for hallucinations). Still, pretty neat.

Where else do you think this may come handy?

--

José Velázquez (MA) is a software architect with over two decades of experience driving digital innovation, consulting for organisations such as the BBC, IBM, and Google. His work sits at the intersection of academia and industry, with a focus on audiovisual preservation, cultural memory, and open, interoperable systems for managing media at scale. Since 2016, José has been an Associate Lecturer on the interdisciplinary Digital Humanities Master's programme at the University of Pablo de Olavide (Seville, Spain.)
