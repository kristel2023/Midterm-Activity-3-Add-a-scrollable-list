# Midterm-Activity-3-Add-a-scrollable-list

package com.example.affirmations

import android.os.Bundle import androidx.activity.ComponentActivity import androidx.activity.compose.setContent import androidx.activity.enableEdgeToEdge import androidx.compose.foundation.layout.fillMaxSize import androidx.compose.foundation.layout.padding import androidx.compose.material3.Scaffold import androidx.compose.material3.Text import androidx.compose.runtime.Composable import androidx.compose.ui.Modifier import androidx.compose.ui.tooling.preview.Preview import com.example.affirmations.ui.theme.AffirmationsTheme import androidx.compose.foundation.layout.Column import androidx.compose.material3.Card import com.example.affirmations.ui.theme.AffirmationsTheme import androidx.compose.foundation.layout.fillMaxWidth import androidx.compose.foundation.layout.height import androidx.compose.material3.MaterialTheme import androidx.compose.material3.Surface import androidx.compose.ui.layout.ContentScale import androidx.compose.ui.platform.LocalContext import androidx.compose.ui.res.painterResource import androidx.compose.ui.res.stringResource import androidx.compose.ui.unit.dp import androidx.compose.foundation.Image import androidx.compose.foundation.lazy.LazyColumn import androidx.compose.foundation.lazy.items

class MainActivity : ComponentActivity() { override fun onCreate(savedInstanceState: Bundle?) { super.onCreate(savedInstanceState) enableEdgeToEdge() setContent { AffirmationsTheme { Surface( modifier = Modifier.fillMaxSize(), color = MaterialTheme.colorScheme.surface ) { AffirmationsApp() } } } }

@Composable
fun AffirmationsApp() {
    AffirmationList(
        affirmationList = Datasource().loadAffirmations(),
    )
}

@Composable
fun AffirmationList(affirmationList: List<Affirmation>, modifier: Modifier = Modifier) {
    LazyColumn(modifier = modifier) {
        items(affirmationList) { affirmation ->
            AffirmationCard(
                affirmation = affirmation,
                modifier = Modifier.padding(8.dp)
            )
        }
    }
}

@Composable
fun AffirmationCard(affirmation: Affirmation, modifier: Modifier = Modifier) {
    Card(modifier = Modifier) {
        Column {
            Image(
                painter = painterResource(affirmation.imageResourceId),
                contentDescription = stringResource(affirmation.stringResourceId),
                modifier = Modifier
                    .fillMaxWidth()
                    .height(194.dp),
                contentScale = ContentScale.Crop
            )
            Text(
                text = stringResource(affirmation.stringResourceId),
                modifier = Modifier.padding(16.dp),
                style = MaterialTheme.typography.headlineSmall
            )
        }
    }
}

@Preview(showBackground = true)
@Composable
private fun AffirmationCardPreview() {
    AffirmationCard(Affirmation(R.string.affirmation1, R.drawable.image1))
}
}
